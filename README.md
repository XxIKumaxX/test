from selenium import webdriver
from selenium.webdriver.common.keys import Keys
import time

class InstagramBot:
    
    def __init__(self, username, password):
        self.username = username
        self.password = password
        self.driver = webdriver.Firefox()

    def closeBrowser(self):
        self.driver.close()

    def login(self):
        driver = self.driver
        driver.get("https://www.instagram.com/")
        time.sleep(2)
        
        #user_name_elem = driver.find_element_by_xpath("//input[@name='username']") #Enter username
        user_name_elem = driver.find_element_by_xpath("/html/body/div[1]/section/main/article/div[2]/div[1]/div/form/div[2]/div/label/input[@name='username']") #Enter username
        user_name_elem.clear()
        user_name_elem.send_keys(self.username)
        
 
        password_elem = driver.find_element_by_xpath("//input[@name='password']") #Enter password
        password_elem.clear()
        password_elem.send_keys(self.password)

        password_elem.send_keys(Keys.RETURN) #enter
