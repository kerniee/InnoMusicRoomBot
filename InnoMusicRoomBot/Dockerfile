# Use the official .NET Core SDK image as the base image
FROM mcr.microsoft.com/dotnet/core/sdk:2.1 AS build-env

# Set the working directory in the container
WORKDIR /app

# Copy the project files into the container
COPY . ./

# Build the C# application inside the container
RUN --mount=type=cache,id=nuget,target=/root/.nuget/packages\
    dotnet publish -c Release -o out

# Use the official .NET Core runtime image as the final image
FROM mcr.microsoft.com/dotnet/core/aspnet:2.1

# Set the working directory in the container
WORKDIR /app

# Copy the published application from the build-env stage to the final image
COPY --from=build-env /app/out .

# Expose the port that your application listens on (adjust as needed)
EXPOSE 80

# Define the entry point for your application
ENTRYPOINT ["dotnet", "InnoMusicRoomBot.dll", "--environment=Production"]