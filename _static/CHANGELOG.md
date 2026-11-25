# Changelog

All notable changes to VizMini2 are documented here.
The format follows Keep a Changelog, and the project uses semantic versioning.

## [1.0.0] - 2026-11-25

### Added
- **VizMini2 for the PC (Linux and Windows):** the same tabs as on the phone, in a window. On Linux, install the `.deb` on Ubuntu 20.04 or newer, or build it as a ROS 2 package and start it with `ros2 run vizmini2 vizmini2` (the first time it takes the domain and the peers from the terminal). It has the demo robot too (Configuration › Start demo, or `vizmini2 --demo`), on that computer only.
- **On Windows 10 and 11** (64-bit): install the `.msi` (for your user, no administrator needed: it asks where, and adds a shortcut on the desktop and in the Start menu) or unzip the `.zip`. Uninstalling it from Settings › Apps keeps your settings, bags and videos. H.264/H.265 video and recording the window use ffmpeg (`winget install ffmpeg`; without it, the app says how to get it), the open and save dialogs are Windows' own, and a notification says when a video is saved (click it to see the video in Explorer).
- **MoveIt tab:** plan and move a robot arm with `move_group`: planning groups and named poses, a slider per joint, moving the gripper in X, Y, Z and around its axes, straight lines, the planner and the planning time, and obstacles. Works with the MoveIt of Humble, Jazzy and newer.
- **Controllers tab (ros2_control):** the controllers of a controller manager with their state; activate, deactivate, configure, load and unload them; move the joints of trajectory and forward command controllers; and the hardware components with their interfaces. Foxy, Humble, Jazzy and newer.
- **Maps tab:** save the map on the robot (Nav2's map_saver or SLAM Toolbox) or download it as PGM and YAML, pause SLAM, clear the costmaps, and draw keepout and speed limit zones published as Nav2 costmap filter masks.
- **Alerts tab:** your own rules on any topic (a value above or below a threshold, or no messages for some seconds) with notifications, also in the background, and the latest notices.
- **PlanSys2 tab:** follow a PlanSys2 plan while it runs, like its terminal monitor: the plan with the state and progress of each action, the actions under way and their performers, the knowledge (instances, predicates, functions and the goal, with what already holds) and the plan log, what the executor does and why. The four together or each one on its own. PlanSys2 4.0.0 and newer (Jazzy, rolling) and the earlier 3.x messages; the demo robot has one too.
- **H.264 and H.265 video topics** (`foxglove_msgs/CompressedVideo` and ffmpeg_image_transport) in the Camera tab and in the 3D view's Image and Camera displays. The demo camera is also published as H.264.
- **Record the screen as a video:** the record button at the top (saved to Movies/VizMini2); on the PC, Record video in the sidebar.
- **Import and export** RViz 2 files, panel layouts (`.json`) and plot layouts (`.xml`), from + and from each tab's menu. Publish panels become buttons, and every tab of a layout comes in as a dashboard of its own.
- **Plot tab:** series over time, XY, state transitions, spectrum and histogram, with formulas and Lua scripts, from topics, bags, CSV files, UDP, MQTT and ZeroMQ.
- **Indicators, GPS map, Behavior tree** (Groot2 with the blackboard, recording and breakpoints, and the Nav2 log), **Message** and **Parameters** tabs.
- **3D view:** Camera, DepthCloud, Effort, Image with annotations, Trajectory (the planned path as a ghost robot) and Planning scene displays, mesh markers, interactive markers, the Select, Measure and Publish point tools, and a MoveIt tool to drag the arm's goal. Image and camera panels can be moved and resized.
- **NavMap display:** EasyNavigation's NavMap maps (`navmap_ros_interfaces/NavMap`) in the 3D view: navigable surfaces on one or several floors, colored by any of their layers (cost, elevation, occupancy…), with the links between floors (stairs, elevators, doors) and live layer updates. RViz files with its plugin are imported and exported.
- **Fixed frame written by hand:** in the RViz tab, type any frame, even one that is not in TF yet, to leave a view ready; the automatic one is used until it appears.
- **Robots on rmw_zenoh_cpp** (Zenoh router in Config › Network), and services, actions, parameters and lifecycle of nodes on rmw_cyclonedds_cpp.
- **Through foxglove_bridge:** topics, services, parameters, actions and the node graph.
- **Find robots** (Config › Network) lists the ROS domains with nodes on the network; tap one to connect.
- **Topic variables:** write `${name}` in any topic and set its value once in Config, to switch every tab to another robot at once.
- **Bags:** direct playback with a shared timeline for every tab.
- **Tabs:** duplicate them, share them as a file and import them (on the PC, right-click a tab to rename, duplicate, delete or export it). Dashboard widgets stay where you drop them and can overlap (a joystick over the 3D view), and the camera and joystick widgets are more compact.
- **Message types the app doesn't bring:** paste their definition (what `ros2 interface show` prints) right where you need them, from the Topics, Message, Services and Actions tabs or from any type list, and use them straight away.
- The Camera tab shows up to four cameras, with their annotations.
- The Nodes tab shows the DDS each node runs on.
- The demo robot has a ros2_control controller manager (deactivating its diff_drive_controller stops it) and its camera also as H.264 video.

### Changed
- **No account needed:** the app opens straight on Home and connects to your robots without one; an account (Google, Microsoft or GitHub) only syncs your robot profiles between devices.
- VizMini2 is free software under the Apache License 2.0.
- New app icon and logo, on the phone and on the PC.
- The app targets Android 16 (API 36).
- Buttons: a long list in a result shows its first values and how many there are (`[0, 1, 1, 2, 3, 5, …] (11)`) instead of just `[11]`.
- Bags: the recording statistics and the playback position update while they run.
- PC: the sidebar's tabs get shorter to fit a small window, and a scrollbar appears when there are more.
- PC: Record video and Ctrl+Shift+R say when ffmpeg is missing and how to install it, and ffmpeg is also found where winget and the usual installs leave it.
- PC: the open and save dialogs have a title and only list the right kind of file, and the extension is added when you type a name without one.
- PC: the installers are about 40 MB smaller (each one only carries its own system's native libraries).
- PC command line: `--tab` also takes a tab's name, and `--import` opens the imported tab.
- The teleop control presets and the buttons of the PC's RViz displays panel (Add, Duplicate, Remove, Rename, Background Color) are translated.

### Fixed
- Services: several calls at once to the same service (also action results) each get their own response, even when the server answers out of order; and ROS 2 clients on Fast DDS, such as `ros2 service call`, can use the services the app serves (the demo robot's).
- PC: any click in a Teleop tab (such as the demo's Drive) gives it the keyboard back after the sidebar or a dialog took it.
- PC: on Windows, the robot's meshes are also found in the local ROS 2 install (`AMENT_PREFIX_PATH`).
- PC: the app no longer creates an `.ihmc` folder in your home folder.
- Crashes at startup on Android 12 and 13, on Android 8 and 9, and when turning the phone to landscape in RViz or Camera.
- With a bag playing in a loop or a restarted simulation, the 3D view stayed frozen: the TF history is cleared when the time jumps back, as in RViz.
- Bags: changing the playback speed made messages arrive in bursts or stall, and some files could make the reader hang.
- After signing in with another account, the profiles of the previous one were uploaded to the new account.
- A mesh used by two displays at once was not shown on the second one, and a plot could freeze the app with very large values.
- Two parts of the app publishing on the same topic at once could send a message twice, and interactive marker buttons could miss a click.
- The demo robot never came to a full stop (its speed kept flickering).

## [0.18.0] - 2026-10-11

### Added
- If you save, delete or sync profiles without an internet connection, the app tells you. The changes stay saved on the phone and are uploaded to the cloud on their own as soon as you are back online; meanwhile, the profiles card in Config shows that there are pending changes.

### Changed
- Once signed in, you can open the app and use your robots without an internet connection, for example connected only to the robot's Wi-Fi, and it now opens right away without waiting for the server. That offline use expires: after a while, the app asks you to connect to the internet for a moment to check your account (without typing your password again), and then you can carry on offline.

### Fixed
- Opening the app without an internet connection could sometimes sign you out, and you had to sign in again once you were back online.
- If the account was deleted from another phone, this one kept getting in with the saved session; it now asks you to sign in again.
- Syncing profiles without a connection stayed on "syncing…" forever.

## [0.17.1] - 2026-10-10

### Fixed
- When signing in with Microsoft or GitHub, the app could stay on the sign-in screen with the loading spinner turning and never move to the main screen; you had to close and reopen it for the session to be picked up. It now goes straight in once you finish on the Microsoft or GitHub page. The same problem affected linking those accounts from Home and confirming account deletion by signing in with them again, and both are fixed too. (Google was not affected.)

## [0.17.0] - 2026-10-10

### Added
- Sign in or sign up with Google, Microsoft or GitHub, without having to create another password. The first time, your account is created with the name and email the provider gives, skipping email verification.
- Link several sign-in methods to the same account from Home. Your account card lists your sign-in methods (email and password, Google, Microsoft and GitHub), each with a button to link or unlink it; so whether you sign in with Google one day and Microsoft the next, you always reach the same account with the same profiles. The last remaining method can't be removed, so you never get locked out of your account.
- If you try to sign in with a provider whose email already has an account, the app warns you and explains to sign in the way you did the first time and link the new method from Home.

### Changed
- The Google, Microsoft and GitHub buttons are on both the sign-in and the sign-up screens.
- Verification and password reset emails arrive in the language you are using the app in.
- When deleting your account, if you signed in with Google, Microsoft or GitHub you confirm by signing in with that service again (previously password only).

## [0.16.0] - 2026-10-09

### Added
- Try the demo without an account, right from the sign-in screen. Home explains what you are seeing and how to create an account to reach your real robots.
- The demo robot has parameters, services (return home, autopilot, add two ints), a Fibonacci action and a lifecycle camera driver, so Nodes, Services, Actions, Lifecycle, Buttons and Node graph can be tried without a real robot. The demo includes Buttons and Lifecycle tabs ready to use.
- The "+" catalog shows a short looping video of each tab type working with the demo robot, in English or Spanish.
- Documentation website with every feature, videos and tutorials, in English and Spanish, opened from Home.
- Privacy policy in English and Spanish, from the sign-in and sign-up screens and from Home.
- Delete your account from Home: your account, name, email and cloud profiles are erased (your password is asked to confirm).
- Contact and bug reports from Home: an email with the app version, Android version and phone model already filled in.
- Support the project from Home, through GitHub Sponsors.

### Changed
- Sign-up asks for first name, last name, email and the password twice, and you can sign in as soon as you confirm your email.
- Tab types are translated in the "+" catalog, on Home and in the names of new tabs (in Spanish, a new camera tab is called "Cámara"). The demo tabs too.
- Without an account the app can only reach the demo robot: the network settings and robot profiles are hidden, and the connection never leaves the phone.
- The quick tour and the privacy policy have their own cards on Home, below What's new.

### Fixed
- A service call could wait until its timeout when the server answered very quickly without a request identity.

## [0.15.0] - 2026-10-06

### Added
- Spanish translation, including this changelog. Pick the language in Config (English, Español or the system default).

### Changed
- Config is tidier: the connection status sits in the Network card (Home keeps the reconnect button) and the changelog lives in Home only.
- The quick tour moved from Home to Config, and the daily tip on Home is gone.
- Smaller, optimized release builds.

## [0.14.0] - 2026-10-02

### Added
- The quick tour covers dashboards, the node graph, the TF tree and Network check, with fresh screenshots.

### Changed
- Node graph also shows participants that don't announce ROS node names, under their DDS participant name (the demo robot included).
- Fresh screenshots in the "+" catalog.

### Fixed
- Remembered robots could be named after a hidden helper node (like the ros2 CLI daemon).
- Joystick labels overlapped in small dashboard widgets.

## [0.13.0] - 2026-09-29

### Added
- Dashboard tab: build your own screen with any tabs as widgets (3D view, several cameras, joystick, buttons, diagnostics…). Move them by dragging, resize them from the corner and remove them in edit mode; they snap to a grid and never overlap.
- The demo includes a ready-made dashboard.
- Node graph and TF tree are now tabs too: add them from "+" or put them in a dashboard.
- Remember robots on this network: robots the app has seen are reached directly next time, even when the Wi-Fi drops multicast traffic.
- Network check in Config: what the phone sees on the network and what to do when the robot doesn't show up.
- Bags compressed with zstd (the default of many ROS 2 setups) can now be opened and played.
- Crash reports also cover crashes inside native code.

### Changed
- A service client can run several calls at the same time, and an action client several goals, each with its own feedback.
- Teleop buttons adapt to small spaces.

### Fixed
- The cloud sync time was shown in the phone's language instead of the app's.

## [0.12.0] - 2026-09-24

### Added
- Nodes, Topics, Services and Actions tabs: browse everything on the network, like the ros2 CLI.
- Topic screen with live echo, rate (Hz) and the nodes that publish and subscribe to it.
- Call any service from a request form, and send action goals with live feedback, result and cancel.
- New "Add tab" catalog: every tab type with a short description and a preview, and a setup page before creating it.
- Quick tour for new users, available from Home at any time.
- Demo mode: a simulated robot runs on the phone (TF, map, laser, camera, diagnostics) and can be driven with teleop. Your setup comes back when you exit.
- Crash reporting, to fix problems faster.

### Changed
- The "+" button opens the new catalog instead of a list.
- Interface texts prepared for upcoming translations.

### Fixed
- Camera tab setup now suggests the image topics found on the network.
- Large image messages are published with much less overhead.

## [0.11.0] - 2026-09-19

### Added
- Bags tab: record topics to MCAP files compatible with `ros2 bag`, play them back to the network (0.5×, 1×, 2×, loop), import, share and delete recordings.
- Node inspector: parameters of any node, editable like `ros2 param` (all types, ranges and read-only flags), plus what it publishes, subscribes to and the services it offers.
- Network graph: nodes and topics like `rqt_graph`, with search and filters, and a live TF tree like `rqt_tf_tree`.
- Nodes count on Home; tap a node to open it in the inspector.
- Robot alerts: notifications when contact with the robot is lost, a diagnostic goes to ERROR or STALE, or a lifecycle node disappears, shuts down or fails.
- Cloud profiles: robot profiles are stored in your account and show up on any phone you sign in on.
- Share a profile as a QR code (full profile or connection only) and import one by scanning it.
- Discovery Server support, like `ROS_DISCOVERY_SERVER`, for large networks, 4G or VPN.

### Changed
- Lifecycle cards can open the node's parameters.
- Recording `/tf_static`, `/map` and `robot_description` keeps their latched (transient local) behaviour.

### Fixed
- Text with accents or "ñ" in parameters and lifecycle states was shown garbled.
- The first service call right after connecting could fail with "does not publish responses".

## [0.10.0] - 2026-09-14

### Added
- New app icon, with a themed (monochrome) variant for Android 13 and later.
- Connection badge in the top bar of every tab; tap it to open Config.
- About section in Config with the app version and the changelog.

### Changed
- Config redesigned in cards, matching the Home tab.
- Consistent look across tabs: rounded cards and fields, tab icons, and status strips in Buttons, Lifecycle and Diagnostics.
- The camera image is shown in a rounded frame, and topic search is easier to reach.

### Fixed
- Discovery peers only reached the first four ROS processes on each peer, so nodes started later could stay invisible.

## [0.9.0] - 2026-09-09

### Added
- Home tab with a welcome screen, live connection summary, ROS graph overview and what's new.
- Lifecycle tab: discover managed nodes on the network, see their current state live and trigger transitions (configure, activate, deactivate, cleanup, shutdown).
- Live ROS graph discovery: topics, services and actions are now listed straight from DDS discovery, like `ros2 topic list`, `ros2 service list` and `ros2 action list`.
- Service and action pickers in the button editor, filled from the discovered graph with their types.
- Full changelog viewer, reachable from the Home tab.
- App version shown on the sign-in screen and on Home.
- "Forgot password?" on the sign-in screen.
- Discovery peers setting (like `ROS_STATIC_PEERS`) for Wi-Fi networks that drop multicast traffic.

### Changed
- The whole interface is now in English, including the default names of existing tabs.
- Redesigned sign-in and sign-up screens.
- Home and Config are now fixed tabs; sign out moved from Config to Home.
- Topic search in RViz and Camera tabs lists every topic on the network instead of probing a fixed set of names.

### Fixed
- Topic search could miss topics with uncommon names or types.
- Service responses are now matched to their request, so two clients calling the same service no longer see each other's replies.

## [0.8.2] - 2026-09-03

### Fixed
- Non-ASCII characters (accents, ñ) in `/rosout` logs and diagnostics were displayed garbled.
- `std_msgs/Empty` messages published from a button were rejected by some subscribers.
- Rotating the device while the 3D view was loading could freeze the app for a few seconds.

## [0.8.1] - 2026-09-01

### Fixed
- Action buttons stayed in "Running…" if the action server went away mid-goal.
- Long service responses were cut off in the result dialog.
- The button grid lost its scroll position when coming back to the tab.

## [0.8.0] - 2026-08-28

### Added
- Buttons tab: configurable buttons that publish a message, call a service or send an action goal, with feedback and cancel.
- Form editor for any message type, with support for nested fields and arrays.
- Custom message, service and action definitions for packages not bundled with the app.
- Hold-to-repeat publishing at a configurable rate.

### Changed
- Diagnostics: only plottable topics are offered in the plot picker.

## [0.7.0] - 2026-08-19

### Added
- Robot profiles: save the connection settings and all tabs under a name and switch between robots in one tap.
- Import and export profiles as JSON files to share them with your team.
- Optional background mode that keeps the ROS 2 node alive with a notification.

### Fixed
- Changing the domain ID did not always drop the old subscriptions.

## [0.6.1] - 2026-08-11

### Fixed
- Support for devices with 16 KB memory pages (Android 15 and later).
- Crash when reopening a camera tab after changing its topic.
- Teleop settings were not saved when the app was closed from the recents screen.

## [0.6.0] - 2026-08-06

### Added
- Diagnostics tab: `/diagnostics` overview grouped by level, topic echo with field filter, and live plots of numeric fields.
- Log viewer for `/rosout` with level filter.
- Physical gamepad support in teleop tabs.

### Changed
- Teleop: safety stop when the network is lost, the gamepad disconnects or the UI stops responding.

## [0.5.0] - 2026-07-27

### Added
- Import `.rviz` configuration files: supported displays, fixed frame and view are restored.
- Robot Model display with meshes (STL, DAE) served over HTTP from the robot.
- Marker and MarkerArray displays, including text.
- Orbit, top-down and first-person views.

### Fixed
- TF frames could flicker when static and dynamic transforms shared a parent.

## [0.4.0] - 2026-07-14

### Added
- Teleop tab with an on-screen joystick publishing `geometry_msgs/Twist`.
- Dual-joystick teleop for holonomic robots and drones.
- Speed presets and per-axis inversion.

## [0.3.0] - 2026-07-03

### Added
- Camera tab for `sensor_msgs/Image` and `CompressedImage`, with automatic topic search.
- Map, Path, Pose and PoseArray displays.
- PointCloud2 display with intensity and RGB coloring.

### Changed
- Smoother 3D rendering with a new physically based renderer.

## [0.2.0] - 2026-06-23

### Added
- Tabs: create, rename and delete your own RViz tabs.
- Config tab with domain ID, node name and network interface selection.
- LaserScan display and TF frame axes.

### Fixed
- The app did not reconnect after the Wi-Fi network changed.

## [0.1.0] - 2026-06-12

### Added
- First internal build.
- Sign in and sign up with email verification.
- 3D view with grid and fixed frame selection.
- Connection to ROS 2 over DDS on the local network.
