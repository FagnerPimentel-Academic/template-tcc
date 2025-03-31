FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt update && apt install --no-install-recommends -y texlive-full

RUN mkdir /build
RUN mkdir /tex
RUN mkdir /output


# pdflatex -shell-escape -synctex=1 -interaction=nonstopmode -file-line-error -output-directory=/build principal.tex &&
# makeglossaries -d /build principal &&
# biber /build/principal &&
# makeindex /build/principal.idx &&
# pdflatex -shell-escape -synctex=1 -interaction=nonstopmode -file-line-error -output-directory=/build principal.tex

WORKDIR /tex