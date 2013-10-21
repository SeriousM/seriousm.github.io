---
layout: post
title:  "Binding to an anonymous type"
date:   2011-03-31 16:48:00
categories: Work Wpf
---

Try to imagine that you have a list of complex classes and you just want to display just a bunch of properties.

For example:
```
Person.Firstname,
Person.Lastname,
Person.Address.District.Name,
Person.Cars[0].Brand,
Person.Cars[1].Brand
```

I was playing around with ValueConverter and found out, that i can return an anonymous type out of the converter and bind it to a textblock’s content.

```
public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
{
  if (value is Persons)
  {
    var persons = (Persons)value;

    var query =
      from person in persons
      let firstname = person.Firstname
      let lastname = person.Lastname
      let districtname = person.Address.District.Name
      let car1 = person.Cars[0].Brand
      let car2 = person.Cars[1].Brand
      select new
      {
        Firstname = firstname,
        Lastname = lastname,
        Districtname = districtname,
        Car1 = car1,
        Car2 = car2
      };

    return query;
  }

  return value;
}
```

Updating the values as you maybe guess don't work, but if you dont want to write complex bindings you can use this technique to archive the result.