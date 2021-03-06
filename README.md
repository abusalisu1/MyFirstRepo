---
page_type: sample
languages:
- csharp
products:
- windows
- windows-uwp
statusNotificationTargets:
- codefirst@microsoft.com
description: "A mini-app for commuters to track drive times to various locations."
---

<!---
  category: MapsAndLocation Data LaunchingAndBackgroundTasks TilesToastAndNotifications FilesFoldersAndLibraries
-->

# Traffic App sample

A mini-app for commuters to track drive times to various locations. The user adds frequently-visited destinations using app-bar buttons or by tapping and holding on the map. Traffic App then provides a quick view into how long it will take to drive to each place from the user's current location, following the fastest route. The user can also flag a particular destination and a background task will periodically monitor traffic to that location, alerting the user when traffic is adding ten minutes or more to the travel time.

> Note - This sample is targeted and tested for Windows 10, version 2004 (10.0; Build 19569), and Visual Studio 2019. If you prefer, you can use project properties to retarget the project(s) to Windows 10, version 1903 (10.0; Build 18362).

This sample runs on the Universal Windows Platform (UWP). 

For a description of the goals and challenges of this project, see the [project overview](ProjectOverview.md).

**Note:** This branch of the repo contains the original version of the sample, which uses a traditional "code-behind" 
architecture. For the Model-View-ViewModel (MVVM) version, see the [MVVM branch](../../tree/MVVM). 

![Traffic app screenshot](/Images/TrafficApp.png)

## Features

Traffic App highlights the following APIs:

* [MapControl](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.maps.mapcontrol.aspx) and [MapItemsControl](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.maps.mapitemscontrol.aspx) ([Windows.UI.Xaml.Controls.Maps](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.maps.aspx))
* [Geolocator](https://msdn.microsoft.com/library/windows/apps/windows.devices.geolocation.geolocator.aspx) ([Windows.Devices.Geolocation](https://msdn.microsoft.com/library/windows/apps/br229921.aspx))
* [MapLocationFinder](https://msdn.microsoft.com/library/windows/apps/windows.services.maps.maplocationfinder.aspx) and [MapRouteFinder](https://msdn.microsoft.com/library/windows/apps/windows.services.maps.maproutefinder.aspx) ([Windows.Services.Maps](https://msdn.microsoft.com/library/windows/apps/windows.services.maps.aspx))
* Background tasks ([Windows.ApplicationModel.Background](https://msdn.microsoft.com/library/windows/apps/windows.applicationmodel.background.aspx))
* Toast notifications ([Windows.UI.Notifications](https://msdn.microsoft.com/library/windows/apps/windows.ui.notifications.aspx))
* Local storage and serialization ([Windows.Storage](https://msdn.microsoft.com/library/windows/apps/windows.storage.aspx))

## Universal Windows Platform development

### Prerequisites

- Windows 10. Minimum: Windows 10, version 1809 (10.0; Build 17763), also known as the Windows 10 October 2018 Update.
- [Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk). Minimum: Windows SDK version 10.0.17763.0 (Windows 10, version 1809).
- [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/) (or Visual Studio 2017). You can use the free Visual Studio Community Edition to build and run Windows Universal Platform (UWP) apps.

To get the latest updates to Windows and the development tools, and to help shape their development, join 
the [Windows Insider Program](https://insider.windows.com).

## Running the sample

Traffic App needs a Bing Maps key to run with full functionality. For security reasons, we can't provide a key as part of the sample - you'll need to get your own at https://www.bingmapsportal.com. Once you have a key, insert it into code in the LocationHelper class constructor and in the MapControl element in MainPage.xaml (you can find these easily by searching the solution for "ServiceToken").

**Note:** The platform target currently defaults to ARM, so be sure to change that to x64 or x86 if you want to test on a non-ARM device. 

The default project is TrafficApp and you can Start Debugging (F5) or Start Without Debugging (Ctrl+F5) to try it out. The app will run in the emulator or on physical devices. If you run in the emulator, be sure to set your location in the location area of the emulator - otherwise, the app won't work correctly.

By default, the app generates four sample locations at random positions around your current location. You can switch to "live mode" instead by changing the commented lines in MainPage.OnNavigatedTo so that locations are loaded from roaming storage.

## Code at a glance

If you're just interested in code snippets for certain API and don't want to browse or run the full sample, check out the following files for examples of some highlighted features:

* [LocationHelper.cs](LocationHelper/LocationHelper.cs#L38)
	- Getting the user's current location using the [Geolocator](https://msdn.microsoft.com/library/windows/apps/windows.devices.geolocation.geolocator.aspx) class.
	- Getting the route, travel time, and distance to a location using the [MapRouteFinder](https://msdn.microsoft.com/library/windows/apps/windows.services.maps.maproutefinder.aspx) class. 
	- Getting the address for a particular position using the [MapLocationFinder](https://msdn.microsoft.com/library/windows/apps/windows.services.maps.maplocationfinder.aspx) class.
	- Displaying a toast notification.
* [MainPage.xaml](TrafficApp/MainPage.xaml#L25) and [MainPage.xaml.cs](TrafficApp/MainPage.xaml.cs#L49): 
	- Using [MapControl](https://msdn.microsoft.com/library/windows/apps/xaml/windows.ui.xaml.controls.maps.mapcontrol.aspx) and [MapItemsControl](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.maps.mapitemscontrol.aspx), handling user gestures on the map. 
	- Displaying locations in the map and list controls using item templates and data binding (including [x:Bind](https://msdn.microsoft.com/library/windows/apps/xaml/mt204783.aspx)).
	- Using a [Flyout](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.flyout.aspx) for location editing, handling the editing experience and edit cancellation.
	- Displaying commands in a [CommandBar](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.commandbar.aspx).
* [TrafficMonitor.cs](TrafficMonitor/TrafficMonitor.cs#L34):
	- Running [background tasks](https://msdn.microsoft.com/library/windows/apps/mt299103.aspx) on a specified interval.
* [LocationDataStore.cs](LocationHelper/LocationDataStore.cs#L40)
	- Generating sample locations at random positions.
	- Serializing data and reading/writing it to roaming storage.
"# MyFirstProject" 
