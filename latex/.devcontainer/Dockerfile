FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt update && apt install --no-install-recommends -y texlive-full

RUN mkdir /build
RUN mkdir /tex
RUN mkdir /output

RUN echo "#!/bin/bash \n \
\n \
echo 'Step 1/5: pdflatex' \n \
pdflatex -shell-escape -synctex=1 -interaction=nonstopmode -file-line-error -output-directory=/build \$1.tex 1> /build/\$1.stdout.pdflatex.log 2> /build/\$1.stderr.pdflatex.log \n \
\n \
echo 'Step 2/5: makeglossaries' \n \
makeglossaries -d /build \$1 1> /build/\$1.stdout.makeglossaries.log 2> /build/\$1.stderr.makeglossaries.log \n \
\n \
echo 'Step 3/5: biber' \n \
biber /build/\$1 1> /build/\$1.stdout.biber.log 2> /build/\$1.stderr.biber.log \n \
\n \
echo 'Step 4/5: makeindex' \n \
openout_any=a makeindex /build/\$1.idx 1> /build/\$1.stdout.makeindex.log 2> /build/\$1.stderr.makeindex.log \n \
\n \
echo 'Step 5/5: pdflatex' \n \
pdflatex -shell-escape -synctex=1 -interaction=nonstopmode -file-line-error -output-directory=/build \$1.tex 1> /build/\$1.stdout.pdflatex.log 2> /build/\$1.stderr.pdflatex.log \n \
\n \
cp /build/*.pdf /output \n \
\n \
grep -n \ 
-e 'Warning:' \ 
-e 'Error:' \ 
-e 'Output written on' \ 
/build/\$1.stdout.pdflatex.log > /output/\$1.output.log \n \
echo 'Done!' \n \
echo 'Output files copied to /output' \n \
echo 'You can found all logs files in /.devcontainer/build' \n \
" > texpdf.sh

RUN chmod +x texpdf.sh

WORKDIR /tex