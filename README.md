# Gali's Package
A library of Vue-js elements, made as practice to be used in a project.
https://www.npmjs.com/package/gali-package

## List of Elements:
* ### Input
<pre>import {GalisInput} from 'gali-package'  </pre>
This is a simple input element. In order to use it, you will have to provide a bound config object under the name 'userInput'.  
<pre>userInput: {  
name: this will be the label for the input.  
type: input's type.  
validation: this field takes a function, which will be used to validate the input's value on change.  
invalidMsg: this field takes a string which will be displayed if the user's input is to fail the validation test.  }</pre>
* ### Form
<pre>import {GalisForm} from 'gali-package'  </pre>
This is a form element, utilizing the Input and Button elements from this package.  It is configured using a bound config object under the name 'userForm'.
<pre>userForm: {  
formBase:[
      {name: input's label,
      type: input's type,
      valiation: validation function for input's value,
      invalidMsg: string which will be displayed if the user's input is to fail the validation test.},
      {Repeat with more entires- each one will create its own input in the form.}],
  submitButton: {
       color: string value, button's color
       isLoading: default should be false. this property can be accessed from the form's handler function to change the button's loading status and toggle it accordingly,
       text: string value, button's text},
  submitErrorMsg: string value, message to be displayed upon a failed form submit attempt (if the user tries to submit, but at least one of their inputs failed validation.)
}</pre>
* ### Loader
<pre>import {GalisLoader} from 'gali-package'  </pre>
This loader element darkens the screen and dislays a loading animaiton. It takes the following properties: 
<pre> isLoading: boolean value </pre>
* ### Button
<pre>import {GalisButton} from 'gali-package'  </pre>
This is a simple button element which takes the following properties:
<pre>text: string value, the text displayed in the button.  
color: string value, the button's color.
isLoading: boolean value, controls the button's loading animation.</pre>
