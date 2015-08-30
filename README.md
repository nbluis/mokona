# Mokona [![Build Status](https://travis-ci.org/robsonbittencourt/mokona.svg?branch=master)](https://travis-ci.org/robsonbittencourt/mokona)
The goal of Mokona is to create layers of abstraction to facilitate selection of elements in tests using the Selenium WebDriver project 

##Pages
If you use the [Page Object pattern](http://martinfowler.com/bliki/PageObject.html) in your tests (i hope so) Mokona offers a way to facilitate the creation of these objects.
For this create a class that will represent the page of your application and have it extend the Mokona class named `MokonaPage`.

```java
public class GooglePage extends MokonaPage {

}
```

##Elements 
Elements should be classes in your project representing the visual elements such as buttons, links, and text fields.
Mokona already has some basic elements of html, as mentioned above. To use them you must use the annotation `@Element`
along with a selector that identifies the element on page. Once declared on the page, no need to instantiate them, this is done automatically.

```java
public class GooglePage extends MokonaPage {
	
	@Element(selector="#lst-ib")
	TextField searchInput;
	
	@Element(selector="[name=\"btnK\"]")
	Button searchButton;

	public void search(String textToSearch) {
	   searchInput.set(textToSearch);
	   searchButton.click(); 
	}

}
```

##Create new Elements
If Mokona does not bring an element that you need to feel the will to create it. Simply create a new class that represents your element and have it extend the Mokona class named `MokonaElement`. Once created you can use it the same way as the native elements of Mokona. Of course, if your new element is generic, feel the will to submit a pull request.

```java
public class MyAwesomeRadioButton extends MokonaElement {

	public void select() {
	   getElement().click();
	}

	public boolean isSelected() {
	   return getElement().isSelected();
	}

}
```

##Configuration
To use Mokona is necessary to create a configuration file in the root of your project. This file should be called mokona.properties. For now the only configuration required is the location of your WebDriver, and the only supported driver is the ChromeDriver. A sample configuration can be seen below: 

```
mokona.webdriver.chrome=src/main/resources/chromedriver
```