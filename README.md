# whisper.cpp_windows
Just an .exe that can be used for those unable to build the excellent [whisper.cpp](https://github.com/ggerganov/whisper.cpp) in Windows. Find it on the Releases page. 

Unzip into a folder, download the [ggml model](https://ggml.ggerganov.com/) of your choice, open up a commandline in the folder, and transcribe away!

Example: ```main -m ggml-model-whisper-small.bin -t 4 -otxt -f file.wav```

## More Info
[OpenAI's Whisper](https://github.com/openai/whisper) is a state of the art auto-transcription model. Unfortunately for some, it requires a GPU to be effective.

[Whisper.cpp](https://github.com/ggerganov/whisper.cpp) is an excellent port of Whisper in C++ that solves the GPU issue. It works quite well with a CPU.

Whisper.cpp is quite easy to compile on Linux & MacOS. Non-technical Windows users may struggle a bit because of a lack of Make command in Windows. Compiling with MingW or Visual Studio will solve this issue. If that sounds too complikcated for you, this exe might be useful.

The .exe is compiled from [this commit](https://github.com/ggerganov/whisper.cpp/commit/83c742f1a78a018c4eac790fabab91f174d92c3a).

You may need to install vcredist_x64. Get it [here](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170).

This exe is provided as is, and is not guaranteed to work on all systems. I've tested it on 5 WIndows 10/11 systems, and it worked on 4 of them. The fifth, where it didn't work was an old system with a lot of issues. Possibly that was the reason for failure.

Not sure if I will be able to release an exe every time Whisper.cpp is updated. This was compiled by a member of my team, and I thought I'd share it.

Usage options are below. For more info, check out OpenAI or Whisper.cpp's repos.

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
