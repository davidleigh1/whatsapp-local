# whatsapp-local
Alerts user when a WhatsApp Web feed includes a local address.  Dedicated to the EMT volunteers of United Hatzalah.

# Purpose
Many EMT volunteers are willing, equipped and ready to respond to local incidents close to their home or place of work, but are unable to keep an active ear on their local EMT radio or dispatch. Nor do they know the name of every street, alleyway or park near their current location.

This app was intended to run as a Browser App or Browser Extension, and will alert the user audibly and visually to any mention of a local street or landmark that appears in a WhatsApp Desktop chat.

# How It Works
1. User can add/save/update the following details in the App:
  1. One or more `Addresses` with a free-text label (e.g. *'Home'* and *'Work'*)
  2. Their `Current Location`.  This can be entered into the App, or user can select one of the saved `Addresses`
  3. The `Alert Range` (distance in miles or km) from their `Current Location` for which user wishes to be alerted
  4. A `Default City` which will be assumed if no city name is found in the WhatsApp feed
4. The App then looks up and stores the geo-coordinates of the user's `Current Location`
5. The App calls the excellent GeoNames.org API and receives a list of all street names within the `Alert Range` from the user's `Current Location`
6. Please note - in dense urban areas with many unique street names, the user may be informed that the maximum available Alert Range is more limited than was requested.
7. The App monitors the WhatsApp feeds in the following way:
  1. Prevents processing of browser tabs which are not WhatsApp Web
  2. Prevents processing of any WhatsApp Web chats not specified in Settings (not currently supported)
  3. Prevents processing of any WhatsApp messages which do not contain:
    * The name of the user's current Town or City
    * Any associated abbreviation, acronym or misspelling which is associated with the name of the user's current Town or City (e.g. map LDN>London or LA>Los Angeles)
    Note: The Town/City requirements can be disabled.  This is useful when only street names are provided in your feed.
  4. Each relevant message is then parsed by a regular expression looking for any string (or sub-string) which matches one or more of the street names falling with the Alert Range.
8. Once a match has been found, one or more of the following should occur (depending on user settings):
  1. A browser / desktop notification appears showing the matched address (and distance from Current Location)
  2. A browser alert() message window pops-up showing the matched address (and distance from Current  Location).  This kind of notification is more aggressive and will also propel the browser to the front of all other windows.
  3. The matched text in the WhatsApp chat will be clearly highlighted (e.g. triple-size fonts, red, bold text and yellow background)
  4. An audio sound is generated
