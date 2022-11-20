# whisper.cpp_windows
Just an .exe for those unable to build the excellent [whisper.cpp](https://github.com/ggerganov/whisper.cpp) in Windows. Will probably work only on x64 PCs. 

## Usage
* Get the zip file from the [Releases page](https://github.com/regstuff/whisper.cpp_windows/releases/tag/v0.0.1). 

* Unzip it into a folder.

* Download a model from [https://ggml.ggerganov.com/](https://ggml.ggerganov.com/) (let's say ggml-model-whisper-small.bin) and save it into the unzipped folder.

* Go into the unzip folder, and launch a command line in it. (Type cmd in the address bar of the explorer window once you're in the folder)

* Make sure your audio file is a wav file with 16000 Hz sample rate. Use ffmpeg to convert if needed: `ffmpeg -i file.mp3 -ar 16000 -ac 1 -b:a 96K -acodec pcm_s16le file.wav`

* Then paste this into the command line (replace file.wav with the actual filename): `main -m ggml-model-whisper-small.bin -t 4 -otxt -f file.wav`

### More Options
-t option decides how many threads to use for computation. Default is 4. Going beyond 8 can actually lower performance!

-l option specifies the language. Full list of languages is [here](https://github.com/openai/whisper#available-models-and-languages).

If you specify the right language, it should transcribe by default. If you do not specify and language, and the audio is not in English, it will translate into English, rather than transcribe.

-otxt option will save a txt file in the same folder as the input wav file, once transcription is done. Other options are -osrt & -ovtt

So, an advanced command would be something like this: `main -m ggml-model-whisper-small.bin -l Japanese -t 4 -otxt -f file.wav`

All usage options are below. For details, check out [OpenAI's Whisper](https://github.com/openai/whisper) or [Whisper.cpp's](https://github.com/ggerganov/whisper.cpp) repos.

```
usage: ./main [options] file0.wav file1.wav ...

options:
  -h,       --help           show this help message and exit
  -s SEED,  --seed SEED      RNG seed (default: -1)
  -t N,     --threads N      number of threads to use during computation (default: 4)
  -p N,     --processors N   number of processors to use during computation (default: 1)
  -ot N,    --offset-t N     time offset in milliseconds (default: 0)
  -on N,    --offset-n N     segment index offset (default: 0)
  -mc N,    --max-context N  maximum number of text context tokens to store (default: max)
  -ml N,    --max-len N      maximum segment length in characters (default: 0)
  -wt N,    --word-thold N   word timestamp probability threshold (default: 0.010000)
  -v,       --verbose        verbose output
            --translate      translate from source language to english
  -otxt,    --output-txt     output result in a text file
  -ovtt,    --output-vtt     output result in a vtt file
  -osrt,    --output-srt     output result in a srt file
  -owts,    --output-words   output script for generating karaoke video
  -ps,      --print_special  print special tokens
  -pc,      --print_colors   print colors
  -nt,      --no_timestamps  do not print timestamps
  -l LANG,  --language LANG  spoken language (default: en)
  -m FNAME, --model FNAME    model path (default: models/ggml-base.en.bin)
  -f FNAME, --file FNAME     input WAV file path
```


## More Info
[OpenAI's Whisper](https://github.com/openai/whisper) is a state of the art auto-transcription model. Unfortunately for some, it requires a GPU to be effective.

[Whisper.cpp](https://github.com/ggerganov/whisper.cpp) is an excellent port of Whisper in C++, which works quite well with a CPU, thereby eliminating the need for a GPU.

Whisper.cpp is quite easy to compile on Linux & MacOS. Non-technical Windows users may struggle a bit because of a lack of Make command in Windows. Compiling with MingW or Visual Studio will solve this issue. If that sounds too complicated for you, this exe might be useful.

The .exe is compiled from [this commit](https://github.com/ggerganov/whisper.cpp/commit/83c742f1a78a018c4eac790fabab91f174d92c3a).

You may need to install vcredist_x64. Get it [here](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170).

This exe is provided as is, and is not guaranteed to work on all systems. I've tested it on 5 WIndows 10/11 systems, and it worked on 4 of them. The fifth, where it didn't work was an old system with a lot of issues. Possibly that was the reason for failure.

Not sure if I will be able to release an exe every time Whisper.cpp is updated. This was compiled by a member of my team, and I thought I'd share it.
