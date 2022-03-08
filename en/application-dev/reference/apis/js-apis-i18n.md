# Internationalization – i18n

> ![icon-note.gif](public_sys-resources/icon-note.gif) **NOTE**
> - The initial APIs of this module are supported since API version 7. Newly added APIs will be marked with a superscript to indicate their earliest API version.
> 
> - This module contains enhanced i18n APIs, which are not defined in ECMA 402.


## Modules to Import

```
import i18n from '@ohos.i18n';
```


## i18n.getDisplayLanguage

getDisplayLanguage(language: string, locale: string, sentenceCase?: boolean): string

Obtains the localized script for the specified language.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | language | string | Yes| Specified language.|
  | locale | string | Yes| Locale ID.|
  | sentenceCase | boolean | No| Whether to use sentence case for the localized script.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | string | Localized script for the specified language.|

- Example
  ```
  i18n.getDisplayLanguage("zh", "en-GB", true);
  i18n.getDisplayLanguage("zh", "en-GB");
  ```


## i18n.getDisplayCountry

getDisplayCountry(country: string, locale: string, sentenceCase?: boolean): string

Obtains the localized script for the specified country.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | country | string | Yes| Specified country.|
  | locale | string | Yes| Locale ID.|
  | sentenceCase | boolean | No| Whether to use sentence case for the localized script.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | string | Localized script for the specified country.|

- Example
  ```
  i18n.getDisplayCountry("zh-CN", "en-GB", true);
  i18n.getDisplayCountry("zh-CN", "en-GB");
  ```


## i18n.isRTL<sup>8+</sup>

isRTL(locale: string): boolean

Checks whether the localized script for the specified language is displayed from right to left.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Description|
  | -------- | -------- | -------- |
  | locale | string | Locale ID.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | boolean | The value **true** indicates that the localized script is displayed from right to left, and value **false** indicates the opposite.|

- Example
  ```
  i18n.isRTL("zh-CN");// Since Chinese is not written from right to left, false is returned.
  i18n.isRTL("ar-EG");// Since Arabic is written from right to left, true is returned.
  ```


## i18n.getSystemLanguage

getSystemLanguage(): string

Obtains the system language.

**System capability**: SystemCapability.Global.I18n

- Return value
  | Type| Description|
  | -------- | -------- |
  | string | System language ID.|

- Example
  ```
  i18n.getSystemLanguage();
  ```


## i18n.getSystemRegion

getSystemRegion(): string

Obtains the system region.

**System capability**: SystemCapability.Global.I18n

- Return value
  | Type| Description|
  | -------- | -------- |
  | string | System region ID.|

- Example
  ```
  i18n.getSystemRegion();
  ```


## i18n.getSystemLocale

getSystemLocale(): string

Obtains the system locale.

**System capability**: SystemCapability.Global.I18n

- Return value
  | Type| Description|
  | -------- | -------- |
  | string | System locale ID.|

- Example
  ```
  i18n.getSystemLocale();
  ```


## i18n.getCalendar<sup>8+</sup>

getCalendar(locale: string, type? : string): Calendar

Obtains a **Calendar** object.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | locale | string | Yes| Valid locale value, for example, **zh-Hans-CN**.|
  | type | string | No| Valid calendar type. Currently, the valid types are as follows: buddhist, chinese, coptic, ethiopic, hebrew, gregory, indian, islamic\_civil, islamic\_tbla, islamic\_umalqura, japanese, and persian. If this parameter is left unspecified, the default calendar type of the specified locale is used.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | [Calendar](#calendar8) | **Calendar** object.|

- Example
  ```
  i18n.getCalendar("zh-Hans", "gregory");
  ```


## Calendar<sup>8+</sup>


### setTime<sup>8+</sup>

setTime(date: Date): void

Sets the date for this **Calendar** object.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | date | Date | Yes| Date to be set for the **Calendar** object.|

- Example
  ```
  var calendar = I18n.getCalendar("en-US", "gregory");
  var date = new Date(2021, 10, 7, 8, 0, 0, 0);
  calendar.setTime(date);
  ```


### setTime<sup>8+</sup>

setTime(time: number): void

Sets the date and time for this **Calendar** object. The value is represented by the number of milliseconds that have elapsed since the Unix epoch (00:00:00 UTC on January 1, 1970).

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | time | number | Yes| Number of milliseconds that have elapsed since the Unix epoch.|

- Example
  ```
  var calendar = I18n.getCalendar("en-US", "gregory");
  calendar.setTime(10540800000);
  ```


### set<sup>8+</sup>

set(year: number, month: number, date:number, hour?: number, minute?: number, second?: number): void

Sets the year, month, day, hour, minute, and second for this **Calendar** object.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | year | number | Yes| Year to set.|
  | month | number | Yes| Month to set.|
  | date | number | Yes| Day to set.|
  | hour | number | No| Hour to set.|
  | minute | number | No| Minute to set.|
  | second | number | No| Second to set.|

- Example
  ```
  var calendar = i18n.getCalendar("zh-Hans");
  calendar.setTime(2021, 10, 1, 8, 0, 0); // set time to 2021.10.1 08:00:00
  ```


### setTimeZone<sup>8+</sup>

setTimeZone(timezone: string): void

Sets the time zone of this **Calendar** object.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | timezone | string | Yes| Time zone, for example, **Asia/Shanghai**.|

- Example
  ```
  var calendar = i18n.getCalendar("zh-Hans");
  calendar.setTimeZone("Asia/Shanghai");
  ```


### getTimeZone<sup>8+</sup>

getTimeZone(): string

Obtains the time zone of this **Calendar** object.

**System capability**: SystemCapability.Global.I18n

- Return value
  | Type| Description|
  | -------- | -------- |
  | string | Time zone of the **Calendar** object.|

- Example
  ```
  var calendar = i18n.getCalendar("zh-Hans");
  calendar.setTimeZone("Asia/Shanghai");
  calendar.getTimeZone(); // Asia/Shanghai"
  ```


### getFirstDayOfWeek<sup>8+</sup>

getFirstDayOfWeek(): number

Obtains the start day of a week for this **Calendar** object.

**System capability**: SystemCapability.Global.I18n

- Return value
  | Type| Description|
  | -------- | -------- |
  | number | Start day of a week. The value **1** indicates Sunday, and value **7** indicates Saturday.|

- Example
  ```
  var calendar = I18n.getCalendar("en-US", "gregory");
  calendar.getFirstDayOfWeek();
  ```


### setFirstDayOfWeek<sup>8+</sup>

setFirstDayOfWeek(value: number): void

Sets the start day of a week for this **Calendar** object.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | value | number | No| Start day of a week. The value **1** indicates Sunday, and value **7** indicates Saturday.|

- Example
  ```
  var calendar = i18n.getCalendar("zh-Hans");
  calendar.setFirstDayOfWeek(0);
  ```


### getMinimalDaysInFirstWeek<sup>8+</sup>

getMinimalDaysInFirstWeek(): number

Obtains the minimum number of days in the first week of a year.

**System capability**: SystemCapability.Global.I18n

- Return value
  | Type| Description|
  | -------- | -------- |
  | number | Minimum number of days in the first week of a year.|

- Example
  ```
  var calendar = i18n.getCalendar("zh-Hans");
  calendar.getMinimalDaysInFirstWeek();
  ```


### setMinimalDaysInFirstWeek<sup>8+</sup>

setMinimalDaysInFirstWeek(value: number): void

Sets the minimum number of days in the first week of a year.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | value | number | No| Minimum number of days in the first week of a year.|

- Example
  ```
  var calendar = i18n.getCalendar("zh-Hans");
  calendar.setMinimalDaysInFirstWeek(3);
  ```


### get<sup>8+</sup>

get(field: string): number

Obtains the value of the specified field in the **Calendar** object.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | field | string | Yes| Value of the specified field in the **Calendar** object. Currently, a valid field can be any of the following: era, year, month, week\_of\_year, week\_of\_month, date, day\_of\_year, day\_of\_week, day\_of\_week\_in\_month, hour, hour\_of\_day, minute, second, millisecond, zone\_offset, dst\_offset, year\_woy, dow\_local, extended\_year, julian\_day, milliseconds\_in\_day, is\_leap\_month.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | number | Value of the specified field. For example, if the year in the internal date of this **Calendar** object is **1990**, the **get("year")** function will return **1990**.|

- Example
  ```
  var calendar = i18n.getCalendar("zh-Hans");
  calendar.setTime(2021, 10, 1, 8, 0, 0); // set time to 2021.10.1 08:00:00
  calendar.get("hour_of_day"); // 8
  ```


### getDisplayName<sup>8+</sup>

getDisplayName(locale: string): string

Obtains the name of the **Calendar** object displayed for the specified locale.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | locale | string | Yes| Locale for which the name of the **Calendar** object is displayed. For example, if **locale** is **en-US**, the name of the Buddhist calendar will be **Buddhist Calendar**.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | string | Name of the **Calendar** object displayed for the specified locale.|

- Example
  ```
  var calendar = i18n.getCalendar("en-US", "buddhist");
  calendar.getDisplayName("zh"); // Obtain the name of the Buddhist calendar in zh.
  ```


### isWeekend<sup>8+</sup>

isWeekend(date?: Date): boolean

Checks whether the specified date in this **Calendar** object is a weekend.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | date | Date | No| Specified date in this **Calendar** object. If this parameter is left unspecified, the system checks whether the current date in the **Calendar** object is a weekend.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | boolean | The value **true** indicates that the date is a weekend, and value **false** indicates a weekday.|

- Example
  ```
  var calendar = i18n.getCalendar("zh-Hans");
  calendar.setTime(2021, 11, 11, 8, 0, 0); // set time to 2021.11.11 08:00:00
  calendar.isWeekend(); // false
  var date = new Date(2011, 11, 6, 9, 0, 0);
  calendar.isWeekend(date); // true
  ```


## PhoneNumberFormat<sup>8+</sup>


### constructor<sup>8+</sup>

constructor(country: string, options?: PhoneNumberFormatOptions)

Creates a **PhoneNumberFormat** object.

**System capability**: SystemCapability.Global.I18n

Parameters
| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| country | string | Yes| Country or region to which the phone number to be formatted belongs.|
| options | [PhoneNumberFormatOptions](#phonenumberformatoptions8) | No| Options of the **PhoneNumberFormat** object.|

- Example
  ```
  var phoneNumberFormat= new i18n.PhoneNumberFormat("CN", {"type": "E164"});
  ```


### isValidNumber<sup>8+</sup>

isValidNumber(number: string): boolean

Checks whether the format of the specified phone number is valid.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | number | string | Yes| Phone number to be checked.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | boolean | The value **true** indicates the phone number format is valid, and value **false** indicates the opposite.|

- Example
  ```
  var phonenumberfmt = new i18n.PhoneNumberFormat("CN");
  phonenumberfmt.isValidNumber("15812312312");
  ```


### format<sup>8+</sup>

format(number: string): string

Formats a phone number.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | number | string | Yes| Phone number to be formatted.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | string | Formatted phone number.|

- Example
  ```
  var phonenumberfmt = new i18n.PhoneNumberFormat("CN");
  phonenumberfmt.format("15812312312");
  ```


## PhoneNumberFormatOptions<sup>8+</sup>

Defines the options for this PhoneNumberFormat object.


| Name| Type| Readable| Writable| Description|
| -------- | -------- | -------- | -------- | -------- |
| type | string | Yes| Yes| Format type of a phone number. The value can be **E164**, **INTERNATIONAL**, **NATIONAL**, or **RFC3966**.<br>**System capability**: SystemCapability.Global.I18n|


## UnitInfo<sup>8+</sup>

Defines the measurement unit information.


| Name| Type| Readable| Writable| Description|
| -------- | -------- | -------- | -------- | -------- |
| unit | string | Yes| Yes| Name of the measurement unit, for example, **meter**, **inch**, or **cup**.|
| measureSystem | string | Yes| Yes| Measurement system. The value can be **SI**, **US**, or **UK**.<br>**System capability**: SystemCapability.Global.I18n|


## Util<sup>8+</sup>


### unitConvert<sup>8+</sup>

unitConvert(fromUnit: UnitInfo, toUnit: UnitInfo, value: number, locale: string, style?: string): string

Converts one measurement unit into another and formats the unit based on the specified locale and style.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | fromUnit | [UnitInfo](#unitinfo8) | Yes| Measurement unit to be converted.|
  | toUnit | [UnitInfo](#unitinfo8) | Yes| Measurement unit to be converted to.|
  | value | number | Yes| Value of the measurement unit to be converted.|
  | locale | string | Yes| Locale used for formatting, for example, **zh-Hans-CN**.|
  | style | string | No| Style used for formatting. The value can be **long**, **short**, or **medium**.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | string | Character string obtained after formatting based on the measurement unit specified by **toUnit**.|

- Example
  ```
  I18n.Util.unitConvert({unit: "cup", measureSystem: "US"}, {unit: "liter", measureSystem: "SI"}, 1000, "en-US", "long");
  ```


## IndexUtil<sup>8+</sup>


### getInstance<sup>8+</sup>

getInstance(): IndexUtil

Creates an **IndexUtil** object.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | locale | string | No| A string containing locale information, including the language, optional script, and region.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | [IndexUtil](#indexutil8) | **IndexUtil** object mapping to the specified locale.|

- Example
  ```
  var indexUtil= i18n.IndexUtil.getInstance("zh-CN");
  ```


### getIndexList<sup>8+</sup>

getIndexList(): Array&lt;string&gt;

Obtains the index list for this **locale** object.

**System capability**: SystemCapability.Global.I18n

- Return value
  | Type| Description|
  | -------- | -------- |
  | Array&lt;string&gt; | Index list for this **locale** object.|

- Example
  ```
  var indexUtil = i18n.getInstance("zh-CN");
  var indexList = indexUtil.getIndexList();
  ```


### addLocale<sup>8+</sup>

addLocale(locale: string)

Adds the index of the new **locale** object to the index list.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | locale | string | Yes| A string containing locale information, including the language, optional script, and region.|

- Example
  ```
  var indexUtil = i18n.getInstance("zh-CN");
  indexUtil.addLocale("en-US");
  ```


### getIndex<sup>8+</sup>

getIndex(text: string): string

Obtains the index of a text object.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | text | string | Yes| **text** object whose index is to be obtained.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | string | Index of the **text** object.|

- Example
  ```
  var indexUtil= i18n.getInstance("zh-CN");
  indexUtil.getIndex("hi"); // Return h.
  ```


## Character<sup>8+</sup>


### isDigit<sup>8+</sup>

isDigit(char: string): boolean

Checks whether the input character string is composed of digits.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | char | string | Yes| Input character.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | boolean | The value **true** indicates that the input character is a digit, and value **false** indicates the opposite.|

- Example
  ```
  var isdigit = Character.isDigit("1"); // Return true.
  ```


### isSpaceChar<sup>8+</sup>

isSpaceChar(char: string): boolean

Checks whether the input character is a space.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | char | string | Yes| Input character.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | boolean | The value **true** indicates that the input character is a space, and value **false** indicates the opposite.|

- Example
  ```
  var isspacechar = Character.isSpaceChar("a"); // Return false.
  ```


### isWhitespace<sup>8+</sup>

isWhitespace(char: string): boolean

Checks whether the input character is a white space.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | char | string | Yes| Input character.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | boolean | The value **true** indicates that the input character is a white space, and value **false** indicates the opposite.|

- Example
  ```
  var iswhitespace = Character.isWhitespace("a"); // Return false.
  ```


### isRTL<sup>8+</sup>

isRTL(char: string): boolean

Checks whether the input character is of the right to left (RTL) language.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | char | string | Yes| Input character.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | boolean | The value **true** indicates that the input character is of the RTL language, and value **false** indicates the opposite.|

- Example
  ```
  var isrtl = Character.isRTL("a"); // Return false.
  ```


### isIdeograph<sup>8+</sup>

isIdeograph(char: string): boolean

Checks whether the input character is an ideographic character.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | char | string | Yes| Input character.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | boolean | The value **true** indicates that the input character is an ideographic character, and value **false** indicates the opposite.|

- Example
  ```
  var isideograph = Character.isIdeograph("a"); // Return false.
  ```


### isLetter<sup>8+</sup>

isLetter(char: string): boolean

Checks whether the input character is a letter.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | char | string | Yes| Input character.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | boolean | The value **true** indicates that the input character is a letter, and value **false** indicates the opposite.|

- Example
  ```
  var isletter = Character.isLetter("a"); // Return true.
  ```


### isLowerCase<sup>8+</sup>

isLowerCase(char: string): boolean

Checks whether the input character is a lowercase letter.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | char | string | Yes| Input character.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | boolean | The value **true** indicates that the input character is a lowercase letter, and value **false** indicates the opposite.|

- Example
  ```
  var islowercase = Character.isLowerCase("a"); // Return true.
  ```


### isUpperCase<sup>8+</sup>

isUpperCase(char: string): boolean

Checks whether the input character is an uppercase letter.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | char | string | Yes| Input character.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | boolean | The value **true** indicates that the input character is an uppercase letter, and value **false** indicates the opposite.|

- Example
  ```
  var isuppercase = Character.isUpperCase("a"); // Return false.
  ```


### getType<sup>8+</sup>

getType(char: string): string

Obtains the type of the input character string.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | char | string | Yes| Input character.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | string | Type of the input character.|

- Example
  ```
  var type = Character.getType("a");
  ```


## i18n.getLineInstance<sup>8+</sup>

getLineInstance(locale: string): BreakIterator

Obtains a [BreakIterator](#breakiterator8) object for text segmentation.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | locale | string | Yes| Valid locale value, for example, **zh-Hans-CN**. The [BreakIterator](#breakiterator8) object segments text according to the rules of the specified locale.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | [BreakIterator](#breakiterator8) | [BreakIterator](#breakiterator8) object used for text segmentation.|

- Example
  ```
  i18n.getLineInstance("en");
  ```


## BreakIterator<sup>8+</sup>


### setLineBreakText<sup>8+</sup>

setLineBreakText(text: string): void

Sets the text to be processed by the [BreakIterator](#breakiterator8) object.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | text | string | Yes| Text to be processed by the **BreakIterator** object.|

- Example
  ```
  iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit.");
  ```


### getLineBreakText<sup>8+</sup>

getLineBreakText(): string

Obtains the text being processed by the [BreakIterator](#breakiterator8) object.

**System capability**: SystemCapability.Global.I18n

- Return value
  | Type| Description|
  | -------- | -------- |
  | string | Text being processed by the **BreakIterator** object.|

- Example
  ```
  iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit.");
  iterator.getLineBreakText(); // Apple is my favorite fruit.
  ```


### current<sup>8+</sup>

current(): number

Obtains the position of the [BreakIterator](#breakiterator8) object in the text being processed.

**System capability**: SystemCapability.Global.I18n

- Return value
  | Type| Description|
  | -------- | -------- |
  | number | Position of the **BreakIterator** object in the text being processed.|

- Example
  ```
  iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit.");
  breakIter.current(); // 0
  ```


### first<sup>8+</sup>

first(): number

Puts the [BreakIterator](#breakiterator8) object to the first text boundary, which is always at the beginning of the processed text.

**System capability**: SystemCapability.Global.I18n

- Return value
  | Type| Description|
  | -------- | -------- |
  | number | Offset to the first text boundary of the processed text.|

- Example
  ```
  iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit.");
  breakIter.first(); // 0
  ```


### last<sup>8+</sup>

last(): number

Puts the [BreakIterator](#breakiterator8) object to the last text boundary, which is always the next position after the end of the processed text.

**System capability**: SystemCapability.Global.I18n

- Return value
  | Type| Description|
  | -------- | -------- |
  | number | Offset of the last text boundary of the processed text.|

- Example
  ```
  iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit.");
  iterator.last(); // 27
  ```


### next<sup>8+</sup>

next(index?: number): number

Moves the [BreakIterator](#breakiterator8) object backward by the specified number of text boundaries if the specified index is a positive number. If the index is a negative number, the [BreakIterator](#breakiterator8) object will be moved forward by the corresponding number of text boundaries. If no index is specified, the index will be treated as **1**.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | index | number | No| Number of text boundaries by which the [BreakIterator](#breakiterator8) object is moved. A positive value indicates that the text boundary is moved backward, and a negative value indicates the opposite. If no index is specified, the index will be treated as **1**.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | number | Position of the [BreakIterator](#breakiterator8) object in the text after it is moved by the specified number of text boundaries. The value **-1** is returned if the position of the [BreakIterator](#breakiterator8) object is outside of the processed text after it is moved by the specified number of text boundaries.|

- Example
  ```
  iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit.");
  iterator.first(); // 0
  iterator.next(); // 6
  iterator.next(10); // -1
  ```


### previous<sup>8+</sup>

previous(): number

Moves the [BreakIterator](#breakiterator8) object to the previous text boundary.

**System capability**: SystemCapability.Global.I18n

- Return value
  | Type| Description|
  | -------- | -------- |
  | number | Position of the [BreakIterator](#breakiterator8) object in the text after it is moved to the previous text boundary. The value **-1** is returned if the position of the [BreakIterator](#breakiterator8) object is outside of the processed text after it is moved by the specified number of text boundaries.|

- Example
  ```
  iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit.");
  iterator.first(); // 0
  iterator.next(3); // 12
  iterator.previous(); // 9
  ```


### following<sup>8+</sup>

following(offset: number): number

Moves the [BreakIterator](#breakiterator8) object to the text boundary after the position specified by the offset. Position of the [BreakIterator](#breakiterator8) object after it is moved to the text boundary after the position specified by the offset.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | offset | number | Yes| Offset to the position before the text boundary to which the [BreakIterator](#breakiterator8) object is moved.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | number | The value **-1** is returned if the text boundary to which the [BreakIterator](#breakiterator8) object is moved is outside of the processed text.|

- Example
  ```
  iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit.");
  iterator.following(0); // 6
  iterator.following(100); // -1
  iterator.current(); // 27
  ```


### isBoundary<sup>8+</sup>

isBoundary(offset: number): boolean

Checks whether the position specified by the offset is a text boundary. If **true** is returned, the [BreakIterator](#breakiterator8) object is moved to the position specified by the offset. If **false** is returned, the [BreakIterator](#breakiterator8) object is moved to the text boundary after the position specified by the offset, which is equivalent to calling [following](#following8)(offset).

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | offset | number | Yes| Position to check.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | boolean | The value **true** indicates that the position specified by the offset is a text boundary, and value **false** indicates the opposite.|

- Example
  ```
  iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit.");
  iterator.isBoundary(0); // true;
  iterator.isBoundary(5); // false;
  ```


## i18n.is24HourClock<sup>8+</sup>

is24HourClock(): boolean

Checks whether the 24-hour clock is used.

**System capability**: SystemCapability.Global.I18n

- Return value
  | Type| Description|
  | -------- | -------- |
  | boolean | The value **true** indicates that the 24-hour clock is used, and value **false** indicates the opposite.|

- Example
  ```
  var is24HourClock = i18n.is24HourClock();
  ```


## i18n.set24HourClock<sup>8+</sup>

set24HourClock(option: boolean): boolean

Sets the 24-hour clock.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | option | boolean | Yes| Whether to enable the 24-hour clock. The value **true** means to enable the 24-hour clock, and value **false** means the opposite.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | boolean | The value **true** indicates that the 24-hour clock is enabled, and value **false** indicates the opposite.|

- Example
  ```
  // Set the system time to the 24-hour clock.
  var success = I18n.set24HourClock(true);
  ```


## i18n.addPreferredLanguage<sup>8+</sup>

addPreferredLanguage(language: string, index?: number): boolean

Adds a preferred language to the specified position on the preferred language list.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | language | string | Yes| Preferred language to add.|
  | index | number | No| Position to which the preferred language is added.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | boolean | The value **true** indicates that the preferred language is successfully added, and value **false** indicates the opposite.|

- Example
  ```
  // Add zh-CN to the preferred language list.
  var language = 'zh-CN';
  var index = 0;
  var success = i18n.addPreferredLanguage(language, index);
  ```


## i18n.removeDisplayLanguage<sup>8+</sup>

removeDisplayLanguage(index: number): boolean

Deletes a preferred language from the specified position on the preferred language list.

**System capability**: SystemCapability.Global.I18n

- Parameters
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | index | number | Yes| Position of the preferred language to delete.|

- Return value
  | Type| Description|
  | -------- | -------- |
  | boolean | The value **true** indicates that the preferred language is deleted, and value **false** indicates the opposite.|

- Example
  ```
  // Delete the first preferred language from the preferred language list.
  var index = 0;
  var success = i18n.removePreferredLanguage(index);
  ```


## i18n.getPreferredLanguageList<sup>8+</sup>

getPreferredLanguageList(): Array<string>

Obtains the preferred language list.

**System capability**: SystemCapability.Global.I18n

- Return value
  | Type| Description|
  | -------- | -------- |
  | Array<string> | Preferred language list.|

- Example
  ```
  var preferredLanguageList = i18n.getPreferredLanguageList();
  ```


## i18n.getFirstPreferredLanguage<sup>8+</sup>

getFirstPreferredLanguage(): string

Obtains the preferred language that best matches the HAP resource.

**System capability**: SystemCapability.Global.I18n

- Return value
  | Type| Description|
  | -------- | -------- |
  | string | Preferred language that best matches the HAP resource.|

- Example
  ```
  var firstPreferredLanguage = i18n.getFirstPreferredLanguage();
  ```
