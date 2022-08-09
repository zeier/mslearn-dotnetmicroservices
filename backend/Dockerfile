# Pull the mcr.microsoft.com/dotnet/sdk:6.0 image and name the image build
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build

WORKDIR /src

# Copy the file named backend.csproj found locally to the /src directory that was just created
COPY backend.csproj .

RUN dotnet restore

# Copy everything in the local working directory to the image
COPY . .

RUN dotnet publish -c release -o /app

# Pull the mcr.microsoft.com/dotnet/aspnet:6.0 image
FROM mcr.microsoft.com/dotnet/aspnet:6.0

WORKDIR /app

# Expose port 80 and 443
EXPOSE 80
EXPOSE 443

# Copy everything from the /app directory of the build image created above into the app directory of this image
COPY --from=build /app .

# Set the entrypoint of this image to dotnet and passes backend.dll as an argument
ENTRYPOINT ["dotnet", "backend.dll"]


##
# Build the image: run "docker build -t pizzabackend ." from the `backend` folder.
#
# This runs the commands in the Dockerfile in the current directory and applies the tag pizzabackend to the resulting image.
#
# Run command "docker images" to check that the image has been created.
##

##
# Run a container: docker run -it --rm -p 5200:80 --name pizzabackendcontainer pizzabackend
#
# --rm Automatically remove the container when it exits
#
# The backend can be reached at "http://localhost:5200/pizzainfo".
##
