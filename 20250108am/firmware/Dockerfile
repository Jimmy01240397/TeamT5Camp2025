FROM debian:latest as builder

RUN apt update && apt install binwalk git python3-pip liblzo2-dev gcc make -y

COPY tpra.bin .

RUN git clone https://github.com/sviehb/jefferson.git /usr/local/share/jefferson && \
    cd /usr/local/share/jefferson && \
    pip install -r requirements.txt --break-system-packages && \
    python3 setup.py install

RUN git clone https://github.com/npitre/cramfs-tools /usr/local/share/cramfs-tools && \
    cd /usr/local/share/cramfs-tools && \
    make && \
    cd ../../bin && \
    ln -s ../share/cramfs-tools/cramfsck . && \
    ln -s ../share/cramfs-tools/mkcramfs .

RUN binwalk --run-as=root -e tpra.bin

FROM debian:latest as release

RUN dpkg --add-architecture armhf

RUN apt update && apt install qemu-user qemu-user-static qemu-system-arm liblzo2-dev gdb-multiarch iproute2 -y

COPY --from=builder /_tpra.bin.extracted/ /tpra/
COPY ldd /tpra/squashfs-root/usr/local/bin/ldd

WORKDIR /tpra/squashfs-root

COPY armlinux_server usr/local/bin
COPY cbash /usr/local/bin/cbash
RUN chmod +x /usr/local/bin/cbash

#ENTRYPOINT ["cbash", "-c"]


