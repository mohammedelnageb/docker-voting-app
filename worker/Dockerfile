
FROM --platform=${BUILDPLATFORM} mcr.microsoft.com/dotnet/sdk:7.0.403 AS build


ARG TARGETPLATFORM
ARG TARGETARCH
ARG BUILDPLATFORM

RUN echo "Building on $BUILDPLATFORM, targeting $TARGETPLATFORM ($TARGETARCH)"

WORKDIR /source

COPY *.csproj .
RUN dotnet restore -a $TARGETARCH

COPY . .


RUN dotnet publish -c Release -o /app -a $TARGETARCH --runtime linux-$TARGETARCH --self-contained false --no-restore


FROM mcr.microsoft.com/dotnet/runtime:7.0.13 AS runtime

WORKDIR /app

COPY --from=build /app .

ENTRYPOINT ["dotnet", "Worker.dll"]
