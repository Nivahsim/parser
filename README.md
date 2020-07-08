# parser
# My own parser:


from bs4 import BeautifulSoup
import requests


url = 'http://mg.uz/org/'
allCompanies = []

for k in range(91):
    req2 = requests.get('http://mg.uz/orgs/cat3001?page=' + str(k))
    soup2 = BeautifulSoup(req2.text, 'lxml')
    ifBuilders = soup2.find_all('div', class_='kart_ban')
    try:

        for j in range(30):
            allCompanies.append(ifBuilders[j].text.strip())
    except:
        IndexError


for i in range(1, 1000000):
    try:
        url2 = url + str(i)
        req = requests.get(url2)
        soup = BeautifulSoup(req.text, 'lxml')
        companyName = soup.find('span', class_='org-name').text
        companyPhone = soup.find('div', class_='kartochka').text
        index = companyPhone.find('-', 75)
        index2 = companyPhone.find('-', 75)
        phone = companyPhone[index-8 : index2 + 11]

        if companyName in allCompanies:
            print('_____________________________________________________\n', companyName)
            print('Номера телефонов:', phone)
            print('Ссылка: ', url2)
    except:
        IndexError
# Made by Nivahsim 08.07.2020
