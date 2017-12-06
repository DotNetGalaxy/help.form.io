---
title: Select
book: userguide
chapter: form-components
slug: select
weight: 90
---
A select field will display a list of values in a drop down list to users. Users can select one of the values.

![16 select](https://cloud.githubusercontent.com/assets/13321142/13097258/3083d2fa-d4e5-11e5-96e9-28759d9a045b.png)

#### Label

The label for this field that will appear next to it.

#### Placeholder

The placeholder text that will appear before an option is selected.

#### Data Source Type

Select the type of data the options will be pulled from.

##### Values

These are the values that will be selected on this field. The Value column is what will be stored in the database and the Label is what is shown to the users.

##### Raw Json

Enter a JSON Array to use. It should be formatted as an array of objects with named properties.

##### URL

Enter a url with a data source in JSON Array format. This can be used to populate a Select list with external JSON values. For example, suppose you wish to populate your select drop down with a list of all States within the U.S. You can use an external JSON array like the following.

```
https://cdn.rawgit.com/mshafrir/2646763/raw/states_titlecase.json
```

And place that within the URL of the select drop down <strong>Data Source URL</strong>. You will then need to provide the <strong>Value Property</strong> as well as change the <strong>Item Template</strong> so that it will pull the right value as well as display correctly within the dropdown. The following image shows how the configuration would look for this particular setup.

![Select URL JSON Source](https://raw.githubusercontent.com/formio/help.form.io/gh-pages/assets/img/userguide/userguide-select-url.png)

This will now turn your select dropdown into a list of available States within the US.

#### Value Property

If Raw JSON or URL is selected, enter the name of the property on the objects that will contain the value that will be stored in the database.

#### Search Query Name

If URL is selected, enter the name of the search query parameter to filter requests with. Example, if your url is `http://api.dogs.com/dogs`, and this option is set to `type`, and the user types `nice` in the select field, then this component will send a request to `http://api.dogs.com/dogs?type=nice` and update the select items with the results. If this option is omitted, no new requests will be made when user enters text in the select field.

#### Item Template

If Raw JSON or URL is selected, use the template field to determine how the values will be displayed in the select box. You can use the **item** variable to access the current object in the array. For example, you can embed the value by using {{ item.value }} in a template.

#### Custom CSS Class

A custom CSS class to add to this component. You may add multiple class names separated by a space.

#### Tab Index

Sets the `tabindex` attribute of this component to override the tab order of the form. See the [MDN documentation](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex\) on `tabindex` for more information on how it works.

![](/assets/img/select-validation.png)

#### Required

If checked, the field will be required to have a value.

#### Dynamic Select Filtering

A very common use case that many people have in forms is to dynamically filter a Select dropdown based on the selection of another select dropdown. The typicaly usecase is a form that provides the Make, Model, and Year of automobiles where when you select the Make dropdown, it filters the Model dropdown for those that are within that Make. This functionality can be achieved using the following method. We will use the Make, Model, Year as an example use case for this docs.

Step 1: Create a Make Resource to hold all of the vehicle makes.
  ![Create Vehicle Resource](https://raw.githubusercontent.com/formio/help.form.io/gh-pages/assets/img/userguide/formio-mmy1.png)
 
 Step 2: Create some Vehicle make records.
  ![Create Vehicle Makes](https://raw.githubusercontent.com/formio/help.form.io/gh-pages/assets/img/userguide/formio-mmy2.png)

Step 3: Create a Model Resource to hold all of the vehicle models.
  ![Create Vehicle Model](https://raw.githubusercontent.com/formio/help.form.io/gh-pages/assets/img/userguide/formio-mmy3.png)

Step 4: Create some Vehicle model records.
  ![Create Vehicle Model](https://raw.githubusercontent.com/formio/help.form.io/gh-pages/assets/img/userguide/formio-mmy3b.png)

Step 5: Create the Vehicle Resource to hold all of the vehicles.
  ![Create Vehicle Resource](https://raw.githubusercontent.com/formio/help.form.io/gh-pages/assets/img/userguide/formio-mmy4.png)

 with the following settings for Make:

Data Resource Type: Resource | Resources: Make  | Value: Make

  ![Vehicle Make Settings](https://raw.githubusercontent.com/formio/help.form.io/gh-pages/assets/img/userguide/formio-mmy5.png)

and the following settings for Model

Data Resource Type: Resource | Resources: Model  | Value: Model  |  Refresh on: Make

Input a Filter Query: data.make={{ data.make }}
  
  ![Vehicle Model Settings](https://raw.githubusercontent.com/formio/help.form.io/gh-pages/assets/img/userguide/formio-mmy6.png)

Step 6: Create a bunch of records within Vehicle resource.
  ![Create Vehicle Records](https://raw.githubusercontent.com/formio/help.form.io/gh-pages/assets/img/userguide/formio-mmy7.png)

Step 7: Create a new form called Vehicle Select
  ![Vehicle Select Form](https://raw.githubusercontent.com/formio/help.form.io/gh-pages/assets/img/userguide/formio-mmy8.png)

Step 8: Add the Make dropdown with the following field settings.

Data Resource Type: Resource | Resources: Make  | Value: Make
 
  ![Make Field](https://raw.githubusercontent.com/formio/help.form.io/gh-pages/assets/img/userguide/formio-mmy9.png)

Step 9: Add the Model dropdown

Data Resource Type: Resource | Resources: Model  | Value: Model  |  Refresh on: Make

Input a Filter Query: data.make={{ data.make }}

  ![Model Field](https://raw.githubusercontent.com/formio/help.form.io/gh-pages/assets/img/userguide/formio-mmy10.png)

Step 10: Add the Year dropdown

Data Resource Type: Resource | Resources: Vehicle  | Value: Year  |  Refresh on: Model

Input a Filter Query: data.make={{ data.make }}&data.model={{ data.model }}
 
  ![Year Field](https://raw.githubusercontent.com/formio/help.form.io/gh-pages/assets/img/userguide/formio-mmy11.png)

You are done! Your form now will dyanamically filter based on what is selected.

