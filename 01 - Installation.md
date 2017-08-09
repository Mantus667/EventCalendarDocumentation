# Installation

It is possible to install the package through Nuget or as an Umbraco package.

Type: `install-package EventCalendar.Umbraco` in your Visual Studio NuGet Package Manager.

![nuget](assets/nuget.png)

The other way is to use the normal Umbraco Package install method with the download found here: https://our.umbraco.org/projects/backoffice-extensions/eventcalendar/

![package](assets/package.png)

If you just want to work with the api then also have a look at the core library:

Type: `install-package EventCalendar.Core` in your Visual Studio NuGet Package Manager.

https://www.nuget.org/packages/EventCalendar.Core/

## Global configuration

The package contains a configuration file for global configuration settings. It is located under App_Plugins/EventCalendar/DefaultConfiguration.json.

It contains settings that are reused on backend and frontend of the package.

It looks like this:
{
	"GoogleMapsApiKey": "",
	"DefaultMapLocation": {
		"Latitude": 40.782865,
		"Longitude": -73.965355
	}
}

*Current settings:*
* GoogleMapsApiKey - used for setting the api key to use google maps features of the package.
* DefaultMapLocation - used to set the default map location for setting the location on locations/organiser.