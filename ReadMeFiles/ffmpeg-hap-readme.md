#### Encoding to Hap from the command line using FFmpeg

For users who prefer working with a command line or need to access advanced encoding settings for Hap the popular FFmpeg library can be used to work with Hap movies.

1.  If this is your first time using FFmpeg you may need to install it on your system, or compile it from source. In either case be sure that Snappy is enabled as part of the binary. If you already have FFmpeg on your system with Snappy enabled, you can skip this step.

    You can check that your version of FFmpeg can encode Hap using

        ffmpeg -encoders | grep hap

    If the last line of output ends with `Vidvox Hap encoder` then you can encode Hap. Otherwise install FFmpeg using one of these methods:

    *   On macOS you can use [Homebrew](https://brew.sh) to install FFmpeg with the following command:

            brew install ffmpeg --with-snappy

    *   The semi-official [Windows FFmpeg downloads](http://ffmpeg.zeranoe.com/builds/) have Snappy support enabled.
    *   Ubuntu Linux and some other distributions have Snappy support enabled
    *   Visit [the FFmpeg wiki](https://trac.ffmpeg.org/wiki/CompilationGuide) for instructions on how to compile FFmpeg for macOS, Windows and Linux. Along with the other options you choose, you must pass `--enable-libsnappy` to the configure script before building.
2.  Invoke FFmpeg to convert your files.
    *   For Hap movies use the following command:

            ffmpeg -i yourSourceFile.mov -c:v hap outputName.mov

    *   For Hap Alpha movies use the following command:

            ffmpeg -i yourSourceFile.mov -c:v hap -format hap_alpha outputName.mov

    *   For Hap Q movies use the following command:

            ffmpeg -i yourSourceFile.mov -c:v hap -format hap_q outputName.mov

    In addition you can also specify the following optional flags that can be used to create Hap movies that are highly optimized for specific playback hardware. You should only use these in extreme cases if you have reached a specific bottleneck when using the default settings.

    *   `-chunks N` (default is 1; N is a number from 1-64 that does not exceed the number of CPU cores in the playback system)

            ffmpeg -i yourSourceFile.mov -c:v hap -format hap_q -chunks 4 outputName.mov

    *   `-compressor snappy` or `-compressor none` (default is snappy; when set to none may marginally reduce CPU usage in exchange for much larger file sizes that are a fixed bit-rate)

            ffmpeg -i yourSourceFile.mov -c:v hap -compressor none outputName.mov