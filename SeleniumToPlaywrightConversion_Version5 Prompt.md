Version 5 :



Context: 

You are an AI Agent and act as a Test Manager to convert the selenium code to playwright Typescript for Leaftabs application

We want ONLY Latest Playwright libraries to implement and supported all browsers



Instructions:



Implementation guidelines:



Playwright version: Latest (stable as of 2025)

Browser: Any compatible browser (headless)

Browser Support: Playwright supports all major browsers — Chromium, Firefox, WebKit

Locators Priority: Playwright's Locator text > label > value> xpath

\[USE] Playwright's Locator text > label > value

\[CRITICAL] : avoid id or name if they have numbers 

\[MANDATORY] : Each method/block has detailed comments

Test file use recommended Playwright **built-in test runner**



Run Instructions :



Install Playwright (if not already) : npm init playwright@latest

Run the test : npx playwright test createLead.spec.ts



Examples:



Input Selenium Code :





package LeafTapsCreateLead;

import org.openqa.selenium.By;

import org.openqa.selenium.WebElement;

import org.openqa.selenium.chrome.ChromeDriver;

import org.openqa.selenium.support.ui.Select;



import io.github.bonigarcia.wdm.WebDriverManager;



public class CreateLead {

&nbsp;	

&nbsp;	public static void main(String\[] args) {

&nbsp;		

&nbsp;		

&nbsp;		// Step 0) Setup the chromedriver using webdrivermanager software

&nbsp;		WebDriverManager.chromedriver().setup();

&nbsp;		



&nbsp;		// Step 1) Launch the chrome browser (Class Name -> ChromeDriver)

&nbsp;		ChromeDriver driver = new ChromeDriver();

&nbsp;		

&nbsp;		// Step 2) Load the URL (http://leaftaps.com/opentaps/control/main) -> get

&nbsp;		driver.get("http://leaftaps.com/opentaps");

&nbsp;		





&nbsp;		// Step 3) Maximize the chrome browser

&nbsp;		driver.manage().window().maximize();

&nbsp;		

&nbsp;		// Step 4) Find the username and type the value (DemoSalesManager)

&nbsp;		driver.findElement(By.id("username")).sendKeys("DemoSalesManager");

&nbsp;		

&nbsp;		// Step 5) Find the password and type the value (crmsfa)

&nbsp;		driver.findElement(By.id("password")).sendKeys("crmsfa");	

&nbsp;		

&nbsp;		// Step 6) Find the login button and click

&nbsp;		driver.findElement(By.className("decorativeSubmit")).click();

&nbsp;		

&nbsp;		// Step 7) Verify the title 

&nbsp;		String title = driver.getTitle();

&nbsp;		System.out.println(title);

&nbsp;		

&nbsp;		// Step 8) Click CRM/SFA link

&nbsp;		driver.findElement(By.linkText("CRM/SFA")).click();

&nbsp;		

&nbsp;		// Step 9) Click Create Lead Link

&nbsp;		driver.findElement(By.linkText("Create Lead")).click();

&nbsp;		

&nbsp;		// Step 10) Find the company name and type the company name

&nbsp;		driver.findElement(By.id("createLeadForm\_companyName")).sendKeys("TestLeaf");

&nbsp;		

&nbsp;		// Step 11) Find the first name and type your name

&nbsp;		driver.findElement(By.id("createLeadForm\_firstName")).sendKeys("Babu");



&nbsp;		// Step 12) Find the last name and type your name

&nbsp;		driver.findElement(By.id("createLeadForm\_lastName")).sendKeys("Manickam");

&nbsp;		

&nbsp;		// Step 12 b) Select the Source dropdown with one of the visible text

&nbsp;		WebElement source = driver.findElement(By.id("createLeadForm\_dataSourceId"));

&nbsp;		Select dd1 = new Select(source);

&nbsp;		dd1.selectByVisibleText("Employee");

&nbsp;		

&nbsp;		// Step 12 c) Select the marketing campaign with one of the value

&nbsp;		WebElement marketing = driver.findElement(By.id("createLeadForm\_marketingCampaignId"));

&nbsp;		Select dd2 = new Select(marketing);

&nbsp;		dd2.selectByValue("9001");



&nbsp;		// Step 13) Click Create Lead Button

&nbsp;		driver.findElement(By.name("submitButton")).click();

&nbsp;		

&nbsp;		// Step 14) Print the new title

&nbsp;		title = driver.getTitle();

&nbsp;		System.out.println(title);

&nbsp;		

&nbsp;		

&nbsp;	}



}



Version 5 Prompt Results;



import { test, expect, chromium } from '@playwright/test';



test('Create Lead - Leaftaps Application', async () => {



&nbsp; // Step 1: Launch Chromium browser in headless mode

&nbsp; const browser = await chromium.launch({ headless: true });



&nbsp; // Step 2: Create new browser context and page

&nbsp; const context = await browser.newContext();

&nbsp; const page = await context.newPage();



&nbsp; // Step 3: Navigate to the Leaftaps application URL

&nbsp; await page.goto('http://leaftaps.com/opentaps/control/main');



&nbsp; // Step 4: Enter the username in the login form

&nbsp; await page.getByLabel('Username').fill('DemoSalesManager');



&nbsp; // Step 5: Enter the password in the login form

&nbsp; await page.getByLabel('Password').fill('crmsfa');



&nbsp; // Step 6: Click on the Login button to authenticate

&nbsp; await page.getByRole('button', { name: 'Login' }).click();



&nbsp; // Step 7: Verify and log the Home Page title

&nbsp; const homePageTitle = await page.title();

&nbsp; console.log('Home Page Title:', homePageTitle);



&nbsp; // Step 8: Click on the "CRM/SFA" link to navigate

&nbsp; await page.getByRole('link', { name: 'CRM/SFA' }).click();



&nbsp; // Step 9: Click on the "Create Lead" link

&nbsp; await page.getByRole('link', { name: 'Create Lead' }).click();



&nbsp; // Step 10: Fill in the Company Name in the Create Lead form

&nbsp; await page.getByLabel('Company Name').fill('TestLeaf');



&nbsp; // Step 11: Fill in the First Name in the Create Lead form

&nbsp; await page.getByLabel('First name').fill('Babu');



&nbsp; // Step 12: Fill in the Last Name in the Create Lead form

&nbsp; await page.getByLabel('Last name').fill('Manickam');



&nbsp; // Step 13: Select "Employee" from the Source dropdown by visible label

&nbsp; await page.locator('select:below(label:text("Source"))').selectOption({ label: 'Employee' });



&nbsp; // Step 14: Select "9001" from Marketing Campaign dropdown by value

&nbsp; await page.locator('select:below(label:text("Marketing Campaign"))').selectOption({ value: '9001' });



&nbsp; // Step 15: Click on the "Create Lead" button to submit the form

&nbsp; await page.getByRole('button', { name: 'Create Lead' }).click();



&nbsp; // Step 16: Print and verify the new page title after lead creation

&nbsp; const leadCreatedTitle = await page.title();

&nbsp; console.log('Lead Created Page Title:', leadCreatedTitle);



&nbsp; // Step 17: Close the browser

&nbsp; await browser.close();

});

