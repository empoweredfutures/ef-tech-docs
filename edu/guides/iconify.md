## Iconify

guide on how to add icons using iconify

---

we use `@iconify/tailwind` to add CSS icons to our frontend, this allows very easy usage and manipulation of these icons through tailwind

first visit https://icon-sets.iconify.design/mdi/ to see the complete collection of material design icons that we have access to in our project

use the search bar to find the icon that matches what you are looking for and click it

a popup will appear that has info about the icon

you'll see a dropdown menu where it says "icon: ", click this and choose the tailwind css option

copy the string and paste it into the `className` attribute of the element where you want the icon to be

it's convention to use the `<i />` element when adding icons, though it's not required

a complete icon would look something like this: `<i className='icon-[mdi--person]' />`

then you are done, the icon will appear in the application

with tailwind you can modify these icons with "text" classes like: `text-xl` and `text-blue-400` etc...
