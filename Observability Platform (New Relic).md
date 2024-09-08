# New Relic

#### How does an observability platform collect?

Through a process called instrumentation.

Instrumentation can be done by adding code to existing code but is not scalable.

Agents are better here, being a small software program installed on the server.

#### Types of Agents in New Relic

APM agents for server-side
Browser agents for client-side
Mobile agents for mobile apps
Infrastructure agents for hosts

#### Types of Monitoring in NR

APM, Infrastructure, Mobile, Browser Monitoring

#### New Relic Database

One of Telemetry DBs

NRDB is used for querying telemetry data fast and schema-less.

Has in-memory cache

#### An API key is required to install NR CLI on local pc.

#### Every profile has its own API key, license key and Account ID.

#### DLL files in the directory after installing agents are used for agents to connect to .net profiler to pull the metrics.

#### Config file is to update configurations of NR and license key is to be updated here.

#### Copy the installed agents files (newrelic.config and run.sh) to app folder.

#### In newrelic.yml, settings can be added like license_key, app_name, agent_enabled, etc...

#### Installing agents via maven is easy to manage and newrelic.yml should be configured inside the directory installed.

#### The best way is to install manually using package manager as installation guide in documentation has downsides like constantly need to update agents, mixing up the app code and NR, resulting in source code a lot larger and CICD slower.

#### Anything that contains or sends data to NR is called an entity.

#### Entities may have one or more than one tag (key-value pair, UUID).
