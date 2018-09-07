FROM microsoft/dotnet:2.2-sdk-alpine3.8 AS build

RUN apk add --no-cache git && \
    git clone https://github.com/LordVeovis/NadekoBot /NadekoBot/src/NadekoBot && \
    cd /NadekoBot/src/NadekoBot && \
    dotnet restore && \
    dotnet build -c Release && \
    dotnet publish -c Release -o /app && \
    rm /app/libopus.so /app/libsodium.dll /app/libsodium.so /app/opus.dll && \
    rm -r /app/runtimes/win* /app/runtimes/osx* /app/runtimes/linux-*

FROM microsoft/dotnet:2.2-runtime-alpine3.8 AS runtime
WORKDIR /app
COPY --from=build /app /app
RUN apk add --virtual=.run-deps --no-cache ffmpeg youtube-dl libsodium opus && \
    ln -s /usr/lib/libopus.so.0 /app/libopus.so && \
    ln -s /usr/lib/libsodium.so.23 /app/libsodium.so

VOLUME ["/app/data"]
CMD ["dotnet", "/app/NadekoBot.dll"]
LABEL maintainer="Simone Esposito <chaufnet@gmail.com>"
