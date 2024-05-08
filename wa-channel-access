from selenium import webdriver
from webdriver_manager.chrome import ChromeDriverManager
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time

# Initialize browser

def initialize_browser():
    chrome_driver = ChromeDriverManager().install()
    driver = webdriver.Chrome(service=Service(chrome_driver))
    driver.get('https://web.whatsapp.com/')
    input("Press Enter after you have logged in into WhatsApp Web.")
    return driver

# Navigate to channel
def navigate_to_channel(driver, channel_name):
    channel_icon_css = "span[data-icon='newsletter-unread-outline'], span[data-icon='newsletter-outline']"
    channel_icon = WebDriverWait(driver, 20).until(
        EC.element_to_be_clickable((By.CSS_SELECTOR, channel_icon_css)))
    channel_icon.click()

    # Step 1: Click on the search bar to start searching
    search_bar = WebDriverWait(driver, 20).until(
        EC.presence_of_element_located((By.XPATH, '//*[@id="app"]/div/div[2]/div[2]/div[1]/span/div/span/div/div/div/div[1]/div/div/div[2]/div[2]/div/div[1]/p')))
    search_bar.click()
    
    # Step 2: Type the name of the channel
    search_bar.send_keys(channel_name)
        
    # Step 3: Click on the channel in the search results
    channel_xpath = f"//span[@class='matched-text _ao3e' and contains(text(), '{channel_name}')]"
    channel = WebDriverWait(driver, 20).until(
        EC.element_to_be_clickable((By.XPATH, channel_xpath)))
    channel.click()

def send_message(driver, message):
    # Write
    textarea = WebDriverWait(driver, 20).until(
        EC.presence_of_element_located((By.XPATH, '//*[@id="main"]/footer/div[1]/div/span[2]/div/div[2]/div[1]/div/div[1]/p')))
    textarea.send_keys(message)

    # Send
    sendbutton = driver.find_element(By.XPATH, '//*[@id="main"]/footer/div[1]/div/span[2]/div/div[2]/div[2]/button/span')
    sendbutton.click()

def main():
    driver = initialize_browser()
    channel_name = "YOUR CHANNEL NAME"
    navigate_to_channel(driver, channel_name)
    message = "Hello, World!"
    send_message(driver, message)
    input() #To keep the window open
   
if __name__ == "__main__":
    main()
