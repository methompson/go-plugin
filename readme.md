# go-plugin
Test Project for Go Plugin Framework

This project's goal is to test the efficacy of using multiple binaries at the same time as a plugin system for a Go project. In C, one might use dlopen or *nix or LoadLibrary in Windows and dlopen functionality seems to exist for Go.

However, I wanted to test having multiple binaries that do specialized tasks running at the same time. Such a process seems like it might be easier for development (though I don't know for certain). I can't say for certain how much slower performance might be.

The core tenet of the project is to have a main web server that accepts requests from the public. This service has several hook points where a plugin can either be accessed to mutate data or to perform some other process. At runtime, the main application would accept a configuration file that tells it which plugins are running. Each plugin has its own configuration file that tells the main program which hooks it's attaching to.

At run time, when a hook is hit by the main program, the main program would send a request to the plugin with whatever data is part of the hook. The plugin should accept the data, perform whatever processing it needs to do and then send a response back.

Such a system is likely to be slower than a dynamically linked library at runtime, especially considering a shared library would allow sharing memory. However, one of the tradeoffs is that the separation of concerns allows a plugin to be isolated from the main program in case of crashes and or malicious intent.