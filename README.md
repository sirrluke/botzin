# botzin - phyton
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.chrome.options import Options
import time

# ⚙️ CONFIGURAÇÕES
INSTAGRAM_USER = "seu_usuario"
INSTAGRAM_PASS = "sua_senha"
TARGET_POST_URL = "https://www.instagram.com/p/CODIGO_DO_POST/"

# 🚀 INICIAR CHROME EM MODO HEADLESS
options = Options()
options.add_argument("--headless")  # Executa sem abrir o navegador
options.add_argument("--disable-blink-features=AutomationControlled")
driver = webdriver.Chrome(options=options)

def login():
    driver.get("https://www.instagram.com/accounts/login/")
    time.sleep(3)
    
    # Preencher usuário e senha
    username_input = driver.find_element(By.NAME, "username")
    password_input = driver.find_element(By.NAME, "password")
    username_input.send_keys(INSTAGRAM_USER)
    password_input.send_keys(INSTAGRAM_PASS)
    password_input.send_keys(Keys.ENTER)
    
    time.sleep(5)

def denunciar_post():
    driver.get(TARGET_POST_URL)
    time.sleep(5)
    
    try:
        # Abrir menu de opções
        menu_button = driver.find_element(By.XPATH, "//button[contains(@aria-label,'Mais opções')]")
        menu_button.click()
        time.sleep(2)

        # Clicar em "Denunciar"
        denunciar = driver.find_element(By.XPATH, "//button[contains(text(),'Denunciar')]")
        denunciar.click()
        time.sleep(2)

        # Selecionar motivo da denúncia (exemplo: discurso de ódio)
        motivo = driver.find_element(By.XPATH, "//button[contains(text(),'É impróprio')]")
        motivo.click()
        time.sleep(2)

        # Confirmar denúncia
        confirmar = driver.find_element(By.XPATH, "//button[contains(text(),'Avançar')]")
        confirmar.click()
        time.sleep(2)

        print("✅ Denúncia enviada.")
    except Exception as e:
        print(f"❌ Erro ao denunciar: {e}")

# 🧠 EXECUÇÃO
login()
denunciar_post()
driver.quit()
