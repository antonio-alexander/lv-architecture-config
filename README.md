# lv-architecture-config

(based from LabVIEW 2015)

This repo will contain multiple solutions for configuration for different use cases. Generally, these "Solutions" are meant to be used as templates, where you'd right click the library and save as into another folder. A short description of each is provided below as well as a link to their respective README if applicable.

All of these configurations work off of the idea that reads will happen more often that writes, and that it's safe for the configuration main to act as a functional global and store the most recent version of the configuration.

As a **disclaimer**, these are obviously super opinionated and to be honest, it's possible to create configurations that are far less complex (and by the same token it's easy to make ones that are far inferior). If it helps you sleep at night, i've came to these patterns through a lot of trial and error; I think these are really good solutions to what I think are common configuration needs.

## lv-config-json

This is meant to be a simple, extendable implementation of a json based configuration that holds atomic versions of one or more configuration within a single file.

For more information, check out [README.md](./source/lv-config-json/README.md)

## lv-config-json-indexable

This is an extension of the lv-config-json except that multiple versions of the same configuration can be stored within the same file and are indexable.

For more information, check out [README.md](./source/lv-config-json-indexable/README.md)
