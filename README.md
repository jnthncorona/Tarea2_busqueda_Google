# Tarea2_busqueda_Google

package com.qalabs.seleniumbasics;

import org.openqa.selenium.By;
import org.openqa.selenium.Keys;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;

import java.util.List;

public class Tarea2 {
    public static void main(String[] args) throws InterruptedException, NullPointerException {
        // Define which browser to use
        String browser = "Chrome";

        // Get correct driver for desire browser
        WebDriver myDriver = WebDriverFactory.getDriver(browser);

        myDriver.get("https://www.google.com/");
        
        WebElement searchButton = myDriver.findElement(By.id("lst-ib"));
        searchButton.sendKeys("qaMinds");
        searchButton.sendKeys(Keys.ENTER);
        //boton next
        WebElement nextButto = myDriver.findElement(By.xpath("//span[@style='display:block;margin-left:53px']"));

        int count = 1;
        do {

        List<WebElement> urlPagina = myDriver.findElements(By.xpath("//a[contains (text (), 'QA Minds')]"));
            List<WebElement> descripcion = myDriver.findElements(By.xpath("//div//span[@class='st']"));
        Iteracion myIteracion = new Iteracion();
        myIteracion.iterar(urlPagina, descripcion);
            Thread.sleep(2000);
            nextButto.click();
            count ++;
        } while (count <2);

        
               




            // Wait some seconds
        Thread.sleep(3000);

            // Quit web driver
        myDriver.quit();


        }


}

class Iteracion {


    public void iterar(List<WebElement> Paginaurl, List<WebElement> Listdescripcion) {
        WebElement element = null;
        for (int index = 0; index < Paginaurl.size(); index++) {
            element = Paginaurl.get(index);
            System.out.println("Titulo del sitio: " + element.getText());
            System.out.println("URL del sitio: " + element.getAttribute("href"));
            for (WebElement e : Listdescripcion) {
                System.out.println("Descripcion de los resultados: " + e.getText());
            }

        }
    }
}

