# test

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
        
    def like_photo_hashtag(self, hashtag):
        driver = self.driver
        driver.get("https://www.instagram.com/explore/tags/"+ hashtag +"/")
        time.sleep(2)
        
        for i in range(1,3): #scroll 2 times
            driver.execute_script("window.scrollTo(0, document.body.scrollHeight);") 
            time.sleep(2)

        #searching for picture link
        hrefs = driver.find_elements_by_tag_name("a") #find photo by a elements from <a href>
        print('1.hrefs >> ', hrefs,'\n')

        pic_hrefs = [elem.get_attribute('href') for elem in hrefs] #The information(from hrefs) that has been changed to href(basic hyperlink)
        print('2.pic_hrefs >> ', pic_hrefs,'\n')


        pic_hrefs = [href for href in pic_hrefs if '/p/' in href]
        print('3.pic_hrefs >> ', pic_hrefs,'\n')
        print(hashtag,'>>',str(len(pic_hrefs)))

        for i in pic_hrefs:
            driver.get(i)
            driver.execute_script("window.scrollTo(0, document.body.scrollHeight);")
            try:
                like_button = driver.find_element_by_xpath('//*[@id="react-root"]/section/main/div/div[1]/article/div[2]/section[1]/span[1]/button')
                like_button.click()
            except:
                time.sleep(2)

    def like_photo_profile_Version1(self, profile_name):
        driver = self.driver
        driver.get("https://www.instagram.com/"+ profile_name +"/")
        time.sleep(2)
        
        for i in range(1,4): #scroll n times
            time.sleep(2)
            driver.execute_script("window.scrollTo(0, document.body.scrollHeight);") 
            time.sleep(2)

        #searching for picture link
        hrefs = driver.find_elements_by_tag_name("a") #find photo by a elements from <a href>
        print('1.hrefs >> ', hrefs,'\n')

        pic_hrefs = [elem.get_attribute('href') for elem in hrefs] #The information(from hrefs) that has been changed to href(basic hyperlink)
        print('2.pic_hrefs >> ', pic_hrefs,'\n')


        pic_hrefs = [href for href in pic_hrefs if '/p/' in href]
        print('3.pic_hrefs >> ', pic_hrefs,'\n')
        print(profile_name,'>>',str(len(pic_hrefs)))

        for i in pic_hrefs:
            driver.get(i)
            driver.execute_script("window.scrollTo(0, document.body.scrollHeight);")
            try:
                like_button = driver.find_element_by_xpath('//*[@id="react-root"]/section/main/div/div[1]/article/div[2]/section[1]/span[1]/button')
                like_button.click()
            except:
                time.sleep(2)
   
    def like_photo_profile_Version2(self, profile_name): #The Best NOW
        driver = self.driver
        driver.get("https://www.instagram.com/"+ profile_name +"/")
        time.sleep(2)
        all_hrefs_use=[]

        
        for i in range(1,2): #scroll 10 times
            driver.execute_script("window.scrollTo(0, document.body.scrollHeight);") 
            time.sleep(3)

            #searching for picture link
            hrefs = driver.find_elements_by_tag_name("a") #find photo by a elements from <a href>
            #print('1.hrefs >> ', hrefs,'\n')
            pic_hrefs = [elem.get_attribute('href') for elem in hrefs] #The information(from hrefs) that has been changed to href(basic hyperlink)
            #print('2.pic_hrefs >> ', pic_hrefs,'\n')
            pic_hrefs = [href for href in pic_hrefs if '/p/' in href]
            #print('3.pic_hrefs >> ', pic_hrefs,'\n')
            #print(profile_name,'>>',str(len(pic_hrefs)))
            time.sleep(10)

            all_hrefs_use.extend(list(set(pic_hrefs)))#extend href

        print('+'*10)
        print('all_hrefs_use >>',str(len(all_hrefs_use)),'\n')
        print('all_hrefs_use >>',all_hrefs_use)

        for i in all_hrefs_use:
            driver.get(i)
            driver.execute_script("window.scrollTo(0, document.body.scrollHeight);")
            time.sleep(2)
            try:
                #like_button_old = driver.find_element_by_xpath('//*[@id="react-root"]/section/main/div/div[1]/article/div[2]/section[1]/span[1]/button')
                like_button = driver.find_element_by_xpath('/html/body/div[1]/section/main/div/div[1]/article/div/div[3]/section[1]/span[1]/button')
                html = driver.page_source
                
                
                if '<svg aria-label="ถูกใจ" class="_8-yf5 " fill="#262626" height="24" viewBox="0 0 48 48" width="24">' in html:
                    like_button.click()
                    print('Done',i)
                else:
                    print('Was done',i)
                
            except:
                print('Error...')
                time.sleep(2)

    def like_photo_profile_Version3(self, profile_name):
        driver = self.driver
        driver.get("https://www.instagram.com/"+ profile_name +"/")
        time.sleep(2)
        
        for i in range(1,2): #scroll 1 times
            driver.execute_script("window.scrollTo(0, document.body.scrollHeight);") 
            time.sleep(5)

        hrefs = driver.find_elements_by_tag_name("a") #find photo by a elements from <a href>
        print('1.hrefs >> ', hrefs,'\n')

        pic_hrefs = [elem.get_attribute('href') for elem in hrefs] #The information(from hrefs) that has been changed to href(basic hyperlink)
        print('2.pic_hrefs >> ', pic_hrefs,'\n')


        pic_hrefs = [href for href in pic_hrefs if '/p/' in href]
        print('3.pic_hrefs >> ', pic_hrefs,'\n')
        print(profile_name,'>>',str(len(pic_hrefs)))

        driver.get(pic_hrefs[0])
        
        try:
            while 1:
                try:
                    like_button = driver.find_element_by_xpath('//*[@id="react-root"]/section/main/div/div[1]/article/div[2]/section[1]/span[1]/button')
                    html = driver.page_source        
                    if '<svg aria-label="ถูกใจ" class="_8-yf5 " fill="#262626" height="24" viewBox="0 0 48 48" width="24">' in html:
                        like_button.click()
                        print('Done',i)
                    else:
                        print('Was done',i)
                    driver.execute_script("window.scrollTo(0, document.body.scrollHeight);")  #scroll 1 times
                    time.sleep(5)
                    driver.find_element_by_xpath('/html/body/div[1]/section/main/div/div[3]/div[2]/div/div/div[1]/div[1]').click()#click next picture
                except:
                    print('Error...')
                    time.sleep(2)
        except:
            print('End..')


    
###########################################################################
#Oparation setting

#Login
andreyIG = InstagramBot("printkuma","ice1452361")
andreyIG.login()
time.sleep(5)

#Option
#andreyIG.like_photo_hashtag('bnk48')
andreyIG.like_photo_profile_Version2('bnk48')

#Close browser
#andreyIG.closeBrowser()

print('success...')

#Reference
#https://www.youtube.com/watch?v=BGU2X5lrz9M

