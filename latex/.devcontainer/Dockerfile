FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt update && apt install --no-install-recommends -y texlive-full

RUN mkdir /build
RUN mkdir /tex
RUN mkdir /output

RUN echo "#!/bin/bash \n \
\n \
echo 'Step 1/5: pdflatex' \n \
pdflatex -shell-escape -synctex=1 -interaction=nonstopmode -file-line-error -output-directory=/build \$1.tex > /build/pdflatex.log \n \
\n \
echo 'Step 2/5: makeglossaries' \n \
makeglossaries -d /build \$1 > /build/makeglossaries.log \n \
\n \
echo 'Step 3/5: biber' \n \
biber /build/\$1 > /build/biber.log \n \
\n \
echo 'Step 4/5: makeindex' \n \
openout_any=a makeindex /build/\$1.idx > /build/makeindex.log \n \
\n \
echo 'Step 5/5: pdflatex' \n \
pdflatex -shell-escape -synctex=1 -interaction=nonstopmode -file-line-error -output-directory=/build \$1.tex > /build/pdflatex.log \n \
\n \
cp /build/*.log /output \n \
" > texpdf.sh

RUN chmod +x texpdf.sh

WORKDIR /tex