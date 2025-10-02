# MQTT Data Structures

## Base Structure & Device Registration

**Root Topic**: `shows/`

### Show Broadcasting

- Each show is broadcast under the base topic using its UUID as the show topic name (referred to as the “current show topic”)
- The DSM client broadcasts a heartbeat under the current show topic every minute

### Device Registration

- Each client connected to the show must register using its per-install UUID
- Device topics follow this pattern: `<base>/<current show>/devices/<uuid>`
- Each device must send a heartbeat to its topic every 30 seconds

## Show Data Broadcasting

The DSM client broadcasts show data to individual property topics under the current show:

**Topic Pattern**: `<base>/<current show>/<property>`

### Required Data Fields

#### `title`

The name of the show as saved on the DSM client

#### `location`

The location of the show as saved on the DSM client

#### `dsmNetworkIP`

The DSM client’s local WiFi IP address

#### `scriptName`

The name of the script as saved on the DSM client

#### `status`

The current status of the show. This field updates whenever the status changes on the DSM

#### `line`

The current line being executed on the DSM client

#### `calledCues`

An array of UUIDs representing all called cues, encoded as a Swift array in text format (requiring syntax parsing on the client side)

#### `timeCalls`

A string field for time-based calls such as “beginners call”

**Behaviour**:

- Value is `nil` when empty or on show initialisation
- When a time-based call is made, this field updates to the enum-decodable equivalent of the call
- Each client is responsible for displaying a full-screen alert when this field updates
- Alerts must include a close button
