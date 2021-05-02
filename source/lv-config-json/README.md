# lv-config-json

This is meant to be a simple, extendable implementation of a json based configuration that holds atomic versions of one or more configuration within a single file.

LabVIEW sucks in that there isn't a native/first-party way to get indented JSON (at least in LV 2015). So bare with the ugly files it outputs even though it's user-readable. JSON, although universal, has some glaring limitations, mostly in the data types it supports. I think the most common one will be filepaths (you'll need to store them as strings and do some translation) and there are some inherent limitations with embedding other configuration typedefs (more on that below).

Because for JSON we have to re-write the file in total, each time, you'll notice that we store (like a functional global) the entire configuration on a shift register and will modify portions of it as necessary but will ALWAYS write the entire configuration to file (post truncation).

## Getting Started

Do the following steps to get started with this template/pattern:

 1. Right click the lv-config-json.lvlib library and save-as; store it in a separate folder.
 2. In the new library, edit public/configuration.ctl cluster type definition to contain your configuration in total (i.e. if you have multiple clusters, include them as type definitions).
 3. Modify private/_globals/fg_path.vi to point to the expected location of the JSON file for your configuration.
 4. Open the type definition under public/_control/command.ctl and add any additional write cases (the read cases will ALWAYS read the entire file).
 5. Open main.vi, add functional code for any additional write cases defined in step #4.
 6. Edit the default configuration constant in main.vi to provide a valid default configuration if none is found; this will be written on first run if no configuration is present.

## Guidelines/Opinions

Below are som guidelines that can help provide guard rails when implementing this pattern:

* BE ABSOLUTELY careful about your data types, think simple, think primitives and don't get clever.
* LabVIEW can't indent JSON natively, get over it.
* It's difficult to __convert__ old JSON configurations into __new__ data types.  LabVIEW will give you an error.
* Keep in mind that the pattern has a strong opinion that there should be a single input and a single output (one to provide information to write and another to provide information to read). In the event you want to ONLY provide a subset of information to write, you'll need to have multiple write cases (see step #4).

## About Migration

Migration isn't explicityly supported by this template, but is totally possible. To accomplish this you'll need to save the previous data type (it doesn't need to be a type definition to be functional). Once you have this data type you can attempt to cast the data type and then convert it.

The above solution isn't great, it's kind of terrible and very open to errors, especially for compatible data types. It's best to store version as some text somewhere and use that as the initial source of truth rather than the data types.
