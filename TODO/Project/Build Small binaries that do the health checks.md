

- Language? Python or C++?

- C++ requires assigned builder per architecture (ARCHx64 and what for ).

- Agent required at the orchestrator (per architecture)

- Builder will requires to pull package from repo.

- Package will be compiled for every commit to the repo.

- The initial configuration will be as plain text, a file in the same folder as the binary. (later it will be also built-in or )

- The packages sent to my service via [DECIDE PROTOCOL] #todo And service will have a listening websocket.

- Package must include 
		- MAC
		- Deployment-version
		- UniqueInstallationIdentifier (How to make sure is not being faked? link hardware-wise?)
		- Verification
		- MESSAGE_CODE
		- Meta-data

- [Optional] If non-sense starts coming in to my service I need to block IP´s (temporarily at first, I need to monitor if it could be a problem somehow. Maybe I might need to be able to escalate if I decide to actually use comunication)

- Do we store (and retrieve) this information for analytics?