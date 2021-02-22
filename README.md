# nbs.js
 Parse NBS (Note Block Song / Note Block Studio)  files
Pull Requests and issues are welcome!!

# Example

```js
const NBS = require("nbs.js")

let song = NBS.loadSong("./song.nbs")

console.log(song)
```

# API

## NBS.loadSong(filename)
Loads a song by given filename/path.
- filename : string
- **Returns:** Song

## NBS.parse(data)
Parses data and returns a new Song.
- data : buffer
- **Returns:** Song

## NBS.Song

### new Song([data])
These properties are added to the song:
- data : object
- data.title : string
- data.author : string
- data.description : string
- data.original_author : string
- data.imported_name : string
- data.tempo : number (ticks per second)
- data.length : number (length of song measured in ticks)
- data.songHeight : number (opennbs says its count of layers, but check song.layers for that)
- data.layers : object<Layer> (layers of the song)

## NBS.Layer

### new Layer()
Creates a new layer

### layer.name
Name of the layer

### layer.volume
Volume of the layer (between 0 and 100)

### layer.notes
Object containing Note. Object's keys are the tick position of the note.

### layer.setNote(tick, note)
Sets a note on tick.
- tick : number
- note : Note

## NBS.Note

### new Note(instrument, key)
These properties are also added to the note:
- instrument : number (0-15, can be found [here][https://opennbs.org/nbs])
- key : number (from 0-87, minecraft supports 33-57, [more info][https://opennbs.org/nbs])

### note.pitch
Decimal number representing the pitch for notchian clients, is set to 0 if _note.key_ is out of support range (33-57)

### note.packet
Returns a [minecraft-protocol][https://github.com/PrismarineJS/node-minecraft-protocol] packet data.
Send to client with name of "sound_effect" to play the note.

## NBS.keyToPitch
Object used for note.pitch, perhaps you can modify it for something

## NBS.instrumentIds
Object used to make minecraft-protocol packet data. Is 1.12.2 as far as i know. Maybe fix this later