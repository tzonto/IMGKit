# IMGKit

Cloned from [csquared](http://github.com/csquared/IMGKit) to fix these bugs:

1. Don't **spawn** new `wkhtmltoimage` and continue execution: wait for them to terminate!

2. Recognize that `TempFile` is a file.

The problem with 1. was that, while `wkhtmltoimage` was still running, the
(only partially) rendered image was being uploaded to S3, causing broken images.

The problem with 2. was that, since `wkhtmltoimage` [does not work with HTML in STDIN](http://code.google.com/p/wkhtmltopdf/issues/detail?id=534),
the HTML must be stored in a temporary file, and the original IMGKit thinks that
[Tempfile instances are not files](https://github.com/csquared/IMGKit/blob/master/lib/imgkit/source.rb#L14).

