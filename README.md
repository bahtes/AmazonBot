# AmazonBot
A simple bot using selenium to buy hard to get amazon items

This bot was developed in java and uses selenium to control a chrome tab and view the amazon link inputted, it will detect when the item in the amazon link has been restocked and purchase it.

Source Code:

    import org.openqa.selenium.By;
    import java.util.Scanner;
    import org.openqa.selenium.WebDriver;
    import org.openqa.selenium.chrome.ChromeDriver;
    import org.openqa.selenium.ie.InternetExplorerDriver;
    import java.io.IOException;

    import java.util.concurrent.TimeUnit;

    public class SelenuimTest {

        public static void main(String[] args) {

                System.out.println("Instructions: ");
                System.out.println();
                System.out.println("For this you will need chrome installed, this program will go onto your inputted amazon link and refresh until there's a restock");
                System.out.println("Enter you email then press enter, then enter your password and press enter, ");
                System.out.println("it will then open a browser window and sign in, after this it will wait for how long you want it to so if there's any two factor auth you can put it in, ");
                System.out.println("it will then load onto the link and keep refreshing until it can buy the item");
                System.out.println("");

                Scanner scanner = new Scanner(System.in);
                System.out.println("Enter Amazon email:");
                String email = scanner.nextLine();
                System.out.println("");
                System.out.println("Enter Amazon password:");
                String password = scanner.nextLine();
                System.out.println("");

                System.out.println("Enter Amazon link:");
                String link = scanner.nextLine();
                System.out.println("");
                System.out.println("Enter how long you want the program to wait for you to do any 2FA:");
                String minutesStr = scanner.nextLine();
                System.out.println("");

                int minutes = Integer.parseInt(minutesStr);

                System.setProperty("webdriver.chrome.driver", "D:\\Java Stuff\\chromedriver_win32\\chromedriver.exe");
                WebDriver driver = new ChromeDriver();
                driver.get("https://www.amazon.co.uk/ap/signin?openid.pape.max_auth_age=0&openid.return_to=https%3A%2F%2Fwww.amazon.co.uk%2Fgp%2Fhelp%2Fcustomer%2Fdisplay.html%3Fie%3DUTF8%26tag%3Dgooghydr-21%26hvadid%3D219760731080%26hvpos%3D%26hvexid%3D%26hvnetw%3Dg%26hvrand%3D11485194446736818452%26hvpone%3D%26hvptwo%3D%26hvqmt%3De%26hvdev%3Dc%26ref%3Dnav_signin&openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&openid.assoc_handle=gbflex&openid.mode=checkid_setup&openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0&");
                driver.manage().window().maximize();

                try {
                    TimeUnit.MILLISECONDS.sleep(500);
                } catch (Exception e) {

                }

                driver.findElement(By.id("ap_email")).sendKeys(email);
                driver.findElement(By.id("continue")).click();

                try {
                    TimeUnit.MILLISECONDS.sleep(500);
                } catch (Exception e) {

                }

                driver.findElement(By.id("ap_password")).sendKeys(password);

                driver.findElement(By.id("signInSubmit")).click();

                try {
                    TimeUnit.MINUTES.sleep(minutes);
                } catch (Exception e) {

                }

                int number = 1;

                driver.get(link);

                while (number == 1) {
                    try {
                        driver.findElement(By.id("add-to-cart-button")).click();
                        number = 0;
                    } catch (Exception e) {
                        driver.get(link);
                    }
                }

                driver.get("https://www.amazon.co.uk/gp/cart/view.html?ref_=nav_cart");

                driver.findElement(By.name("proceedToRetailCheckout")).click();
                driver.findElement(By.name("placeYourOrder1")).click();
            }
        }
