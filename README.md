# Product Search Automation

This program automates the process of searching and narrowing down the users result to a certain degree.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

The first thing to do is to download the lastest version selenium.jar and apache POI.jar files. Now add these jar files in the project library as "external jar files".


### Import library files

Import the necessary package file.

```
package pack;

```

Import the necessary library files to initialize objects of classes declared in these library files

```

	import java.io.*;
	import java.util.*;

	import org.apache.poi.*;
	import org.apache.poi.xssf.usermodel.XSSFSheet;
	import org.apache.poi.xssf.usermodel.XSSFWorkbook;
	
	import org.jsoup.Jsoup;
	import org.jsoup.nodes.Document;
	import org.jsoup.nodes.Element;
	import org.jsoup.select.Elements;

	import org.openqa.selenium.By;
	import org.openqa.selenium.JavascriptExecutor;
	import org.openqa.selenium.WebDriver;
	import org.openqa.selenium.WebElement;
	import org.openqa.selenium.chrome.ChromeDriver;
	import org.openqa.selenium.support.ui.Select;
	import org.openqa.selenium.support.ui.WebDriverWait;

```

## Running the tests

To start the automation process, Run the source code on eclipse (I have eclipse 4.13 installed). Before you run the source code, add 
the external jar files and also import necessary library files. To run the code, select Run from the menu -> Run As configuration
->Enter project name as "SearchAmazon" and main class as "pack.SearchAmazon".

### Initialization of Chrome WebDriver

The Chrome driver is created by setting the system property to the chrome driver location. This is done by:

```

       System.setProperty("webdriver.chrome.driver", "chromedriver\\chromedriver.exe");
       WebDriver driver=new ChromeDriver();

```

### maximizing the browser window

The window is made to fit the screen.

```
	driver.manage().window().maximize();

```

## Deployment

Here is the code that opens 'amazon.in' and automates the process of searching for wrist watches and narrowing the search by applying filters such as "Brand",
"Analogue","25% discount or more" and "material".

```
	driver.get("https://www.amazon.in");
        WebElement Dropdown= driver.findElement(By.cssSelector(".nav-search-dropdown"));
        Dropdown.click();
        Select drpdown= new Select(Dropdown);
        drpdown.selectByIndex(41);              
        WebElement searchBox=driver.findElement(By.cssSelector(("#twotabsearchtextbox")));
        searchBox.sendKeys("Watches");
        WebElement searchButton=driver.findElement(By.cssSelector((".nav-search-submit")));
        searchButton.click();
        
        WebElement Element = driver.findElement(By.xpath("//*[@id='brandsRefinements']/ul/li[2]"));
        js.executeScript("window.scrollBy(0,500)");
        Element=driver.findElement(By.linkText("Titan"));												
        Element.click();
        
        new WebDriverWait(driver,20);
        js.executeScript("window.scrollBy(0,500)");
        Element=driver.findElement(By.linkText("25% Off or more"));												
        Element.click();
        
        new WebDriverWait(driver,20);
        js.executeScript("window.scrollBy(0,550)");
        Element=driver.findElement(By.linkText("Analogue"));												
        Element.click();
        
        new WebDriverWait(driver,20);
        js.executeScript("window.scrollBy(0,550)");
        Element=driver.findElement(By.linkText("Leather"));												
        Element.click();
        driver.close();

```
### Exporting data from the webpage to an Excel sheet

This section of the code pulls the data from the search result and writes it into an excel sheet. Only the product description and price is stored.

```
File file = new File("Product_Details.xlsx");
        XSSFWorkbook wb = new XSSFWorkbook();
        XSSFSheet sh = wb.createSheet("Product_Details");
        sh.createRow(0).createCell(0).setCellValue("Product");
        sh.getRow(0).createCell(1).setCellValue("Price");
        FileOutputStream fos = new FileOutputStream(file);
        wb.write(fos);
        int i=0;
        Document Doc= Jsoup.connect("https://www.amazon.in/s?k=Watches&i=watches&bbn=1350387031&rh=p_89%3ATitan%2Cp_n_pct-off-with-tax%3A2665400031%2Cp_n_feature_seven_browse-bin%3A1480900031%2Cp_n_material_browse%3A1480907031&dc&qid=1575208922&rnid=1480889031&ref=sr_nr_p_n_material_browse_2").get();
        Elements temp= Doc.select("div.a-size-base-plus a-color-base a-text-normal");
        for(Element Name:temp)
        {
        	i++;
        	System.out.println(i+" "+ Name.getElementsByTag("a").first().text());
        	
        }
```
I am having deficulties in pulling the data into the excel sheet.


### Built With

* [Java](https://go.java/index.html) - The object oriented programming language.
* [Selenium](https://selenium.dev/about/) - The portable framework for web app testing.


## Author

* **Rahul Rubugunday** - *developer* 

## Acknowledgments

* This project is my first attempt in selenium webdriver coding. I wasn't aware that selenium would be fun to code, it was a good experience.
* This project has inspired me to learn more. I would like to thank Cubereum for this assignment and this oppertunity.
* This has a roller coaster ride for the past 48 hours. If I am given a chance, I would give my 100%.
