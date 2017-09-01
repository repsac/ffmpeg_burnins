# ffmpeg_burnins
This module provides an API to construct the filter flags used by `ffmpeg` to generate burnins on media.

Usage Example
```python
#!/usr/local/bin/python3
import ffmpeg_burnins

# instantiate the class
b = ffmpeg_burnins.Burnins('source.mov')

# options are {} based, but using the provided classes you have the convenience of having defaults
# unsupported keys will raise an exception
options = ffmpeg_burnins.TextOptions(font_size=48)
b.add_text('Top Center', ffmpeg_burnins.Align.TOP_CENTERED,
           options=options)

# setting the opacity to 50%
options['opacity'] = 0.5
b.add_text('Bottom Center@0.5', ffmpeg_burnins.Align.BOTTOM_CENTERED,
           options=options)

options = ffmpeg_burnins.TextOptions(font_size=48, x_offset=100)
b.add_text('Bottom+100', ffmpeg_burnins.Align.BOTTOM_LEFT,
           options=options)

# the same options instance can be re-used
options['x_offset'] = 50
b.add_text('Top Right+50', ffmpeg_burnins.Align.TOP_RIGHT,
           options=options)
b.add_text('Bottom Right+50', ffmpeg_burnins.Align.BOTTOM_RIGHT,
           options=options)

# frame numbers utilize their own options class
options = ffmpeg_burnins.FrameNumberOptions(
    font_size=48,
    frame_offset=101,
    x_offset=100
)
b.add_frame_numbers(ffmpeg_burnins.Align.TOP_LEFT, options=options)

# you can either generate the command string (without subprocessing)
print(b.command('test.mov', overwrite=True))

# or render the burnins to a new media file
b.render('test.mov', overwrite=True)
```

Current implemtation is built for Python 3 and requires PIL to be installed.
