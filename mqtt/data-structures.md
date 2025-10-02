# MQTT data structures

## The base & devices
- Our root topic is shows/
- Each show can be 'broadcasted' under the base topic by creating a show topic named the UUID of the show (the current show topic)
- Every minute the DSM client brodcasts a heartbeat under the current show topic
- Each client connected to the show should use it's per-install UUID to create a topic under <base>/<current show>/devices/<uuid>
- A heartbeat should be sent to this topic every 30 seconds 

## Shows
- Following the previous remarks, the DSM client should broadcast the show data to <base>/<current show>/<property>
- The following data fields are required:
    - name
    - location
    - dsmIP
    - scriptName
    - status
    - line
    - calledCues
    - timeCalls
- Field Name: The name of the show as saved on the DSM client
- Field Location: The location of the show as saved on the DSM client
- Field dsmIP: The DSM client local wifi IP
- Field scriptName: The name of the script as saved on the DSM client
- Field status: The status of the show. The field updates on status changes from the DSM
- Field line: The current line of the DSM client 
- Field calledCues: The UUIDs of all the called cues. Swift array encoded as text. Syntax passing.
- Field timeCalls: A string field. Value is nil when empty and on show init. When a time based call is made, such as a "begginers call", this field is updated to the enum decodable equivalent of the call. Each client is responsoble for shoing a full screen alert when this updates - and a close button. 
