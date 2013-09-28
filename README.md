#HistoDB

A peer-to-peer synchronizable database that runs in the browser and on Node.js.

##Design goals
- **no timestamps**: history based 3-way merging
- **distributed**: merging does not require a central server
- **no change tracing**: change tracing is not necessary - support diff computation on the fly
- **data agnostic**: leave diff and merge of the actual data to plugins
- **be small**: only implement the functional parts of syncing - leave everything else to the application (transport, persistence)
- **sensitive defaults**: have defaults that *just work* but still support custom logic (e.g. for conflict resolution)

HistoDB implements a simple core that allows local commits of data that can be merged with remote commits following three-way-merging semantics.

The architecture is heavily inspired by git and uses a commit graph that is merged between collaborating HistoDB instances.

HistoDB itself is agnostic to the type of data it tracks.
It only receives a string representation of a commits' data.
This representation could be a serialized form of the actual data or just a hash of the data which is stored separately.
Pluggable modules are responsible for implementing custom data types that can be synchronized.
This includes efficient storage across commits and implementation of merging and conflict resolution logic.

Possible data types could be:

- tree/file system (this would effectively be git)
- raw text (including line-wise merging)
- spreadsheets
- blog post objects
- ...

##Contributors
This project was created by Mirko Kiefer ([@mirkokiefer](https://github.com/mirkokiefer)).