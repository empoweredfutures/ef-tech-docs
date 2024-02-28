## Azure Static Images

guide on how to add images

---

we use azure to host all of our static images, this means that there is no `/public/images` or `/public/assets` like in other projects

if you need to create a new image resource you'll need to use the [storage manager](https://github.com/empoweredfutures/storage-manager) application

clone the repo locally and view the instructions in the README for running it

once it's running and you're on the application home screen (http://localhost:5173/) you'll want to choose a folder that you'll upload your file into

you should be uploading static images to the `*-static` folders, so this would be `mp-static` for the mentorship platform and `tma-static` for the task management app

once in the folder you want you can simply choose upload file from the top right

the file name should be short but descriptive and cannot be the same name as an existing image or it will be overwritten

the file name should also be `kebab-case` and be of `jpeg` or `png` types

additionally if the image is very large (in pixel count) and thus large (in file size) then it's a good idea to scale the image down

the software [GIMP](https://www.gimp.org/) has already been used to scale down images that were larger than 1000px wide to meet the 1000px max width

1000px max width is an arbitrary limit for the sake of faster load times for our users and less data transferred from the storage

once your image is uploaded you can then move to the mentorship platform project

in the mentorship platform you'll find an `images` folder in `./src`, here is where you should create your image reference

create a file that has the same name as the image file but with .ts or .tsx as the file extension

call the `createAzureImg` function from `~/util/azure-img` and pass it the name of the image file you uploaded

name the return value very similar (if not the exact same name but in PascalCase) to the image file name and export it (do not use default exports)

this return value is a React component that renders an `<img />` element but with the `src` prop already filled out correctly, you'll still have access to all the attributes/props that you normally would if it was just a regular `<img />`

then you're done, you can use that React component as you normally would and have your image in the application
