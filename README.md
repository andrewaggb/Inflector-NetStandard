# Inflector NetStandard

Inflector is a simple lightweight .NET netstandard class library enabling you to pluralize, singularize, 
titleize (...) words in a specific culture.

#### Pluralize

Singular to plural word conversion.

```csharp

// using extension methods
Inflector.SetDefaultCultureFunc = () => Thread.CurrentThread.CurrentUICulture; // must be setled before using extension methods
...
var cats = "cat".Pluralize(); // produces "cats" (assuming the default culture setled early is english)

// using Inflector class
var inflector = new Inflector(new CultureInfo("en"));
var cats = inflector.Pluralize("cat"); // produces: cats

```

#### Singularize 

Plural to singular word conversion.

```csharp

// using extension methods
Inflector.SetDefaultCultureFunc = () => Thread.CurrentThread.CurrentUICulture; // must be setled before using extension methods
...
var homem = "homens".Singularize(); // produces: homem (assuming the default culture setled early is portuguese)

// using Inflector class
var inflector = new Inflector(new CultureInfo("pt"));
var homem = inflector.Singularize("homens"); // produces: homem

```

#### Capitalize 

Capitalizes the first char and lowers the rest of the string.

```csharp

var sentence = "the quick brown FOX jumps over the lazy dog".Capitalize();
// produces: The quick brown fox jumps over the lazy dog

```

#### Uncapitalize 

Lowers the first char and leaves the remaining text unchanged.

```csharp

var sentence = "The quick brown FOX jumps over the lazy dog".Uncapitalize();
// produces: the quick brown FOX jumps over the lazy dog

```

#### Dasherize 

TBD

#### Pascalize

TBD

#### Camelize 

TBD

#### Titleize 

TBD

#### Underscore 

TBD

#### Humanize 

TBD


#### Creating new culture grammatical rules 

Example for english culture rules:

```csharp
    public class EnglishCultureRules : CultureRules
    {
        public EnglishCultureRules() :
            base( plurals => plurals
                              .Add("$", "s")
                              .Add("s$", "s")
                              .Add("(ax|test)is$", "$1es")
                              .Add("(octop|vir|alumn|fung)us$", "$1i")
                              .Add("(alias|status)$", "$1es")
                              .Add("(bu)s$", "$1ses")
                              .Add("(buffal|tomat|volcan)o$", "$1oes")
                              .Add("([ti])um$", "$1a")
                              .Add("sis$", "ses")
                              .Add("(?:([^f])fe|([lr])f)$", "$1$2ves")
                              .Add("(hive)$", "$1s")
                              .Add("([^aeiouy]|qu)y$", "$1ies")
                              .Add("(x|ch|ss|sh)$", "$1es")
                              .Add("(matr|vert|ind)ix|ex$", "$1ices")
                              .Add("([m|l])ouse$", "$1ice")
                              .Add("^(ox)$", "$1en")
                              .Add("(quiz)$", "$1zes"),
                 singulars => singulars
                                  .Add("s$", "")
                                  .Add("(n)ews$", "$1ews")
                                  .Add("([ti])a$", "$1um")
                                  .Add("((a)naly|(b)a|(d)iagno|(p)arenthe|(p)rogno|(s)ynop|(t)he)ses$", "$1$2sis")
                                  .Add("(^analy)ses$", "$1sis")
                                  .Add("([^f])ves$", "$1fe")
                                  .Add("(hive)s$", "$1")
                                  .Add("(tive)s$", "$1")
                                  .Add("([lr])ves$", "$1f")
                                  .Add("([^aeiouy]|qu)ies$", "$1y")
                                  .Add("(s)eries$", "$1eries")
                                  .Add("(m)ovies$", "$1ovie")
                                  .Add("(x|ch|ss|sh)es$", "$1")
                                  .Add("([m|l])ice$", "$1ouse")
                                  .Add("(bus)es$", "$1")
                                  .Add("(o)es$", "$1")
                                  .Add("(shoe)s$", "$1")
                                  .Add("(cris|ax|test)es$", "$1is")
                                  .Add("(octop|vir|alumn|fung)i$", "$1us")
                                  .Add("(alias|status)es$", "$1")
                                  .Add("^(ox)en", "$1")
                                  .Add("(vert|ind)ices$", "$1ex")
                                  .Add("(matr)ices$", "$1ix")
                                  .Add("(quiz)zes$", "$1"),
                 irregulars => irregulars
                                   .Add("person", "people")
                                   .Add("man", "men")
                                   .Add("child", "children")
                                   .Add("sex", "sexes")
                                   .Add("move", "moves")
                                   .Add("goose", "geese")
                                   .Add("alumna", "alumnae"),
                 uncountables => uncountables
                                     .Add("equipment")
                                     .Add("information")
                                     .Add("rice")
                                     .Add("money")
                                     .Add("species")
                                     .Add("series")
                                     .Add("fish")
                                     .Add("sheep")
                                     .Add("deer")
                                     .Add("aircraft"),
                 number =>
                 {
                     var numberString = number.ToString();
                     int nMod100 = number%100;

                     if (nMod100 >= 11 && nMod100 <= 13)
                     {
                         return numberString + "th";
                     }

                     switch (number%10)
                     {
                         case 1:
                             return numberString + "st";
                         case 2:
                             return numberString + "nd";
                         case 3:
                             return numberString + "rd";
                         default:
                             return numberString + "th";
                     }
                 })
        {
        }
    }

```


---
Distributed as a NuGet package [here](https://www.nuget.org/packages/Inflector.Portable).


---
This library is based on original work by Scott Kirkland (https://github.com/srkirkland/Inflector) and Abel Pereira (https://github.com/abelepereira/Inflector-Portable)
