'''
import requests
from selenium import webdriver
import time

driver = webdriver.PhantomJS(executable_path="phantomjs.exe")
driver.get( 'http://bioinformatica.mty.itesm.mx:8080/Biomatec/SurvivaXvalidator.jsp')

Head_JSP = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 6.1; WOW64; rv:40.0) Gecko/20100101 Firefox/40.0',
    'Referer': 'http://bioinformatica.mty.itesm.mx:8080/Biomatec/SurvivaX.jsp'}
url = 'http://bioinformatica.mty.itesm.mx:8080/Biomatec/SurvivaXvalidator.jsp'
data = {
    'geneinputid':"symbol",
    'genes':"CDKN2AIP",
    'tissue':"Hematologic",
    'database':"128",
    'duplicates':"mean",
    'datasource':"raw",
    'send':"SurvExpress Analysis"
}

loginhtml = requests.post(url, data=data, headers=Head_JSP)

loginhtml.content

time.sleep(1)
driver.
print driver.page_source.encode('gbk','ignore')
#print loginhtml.text

'''


import os
from selenium.webdriver.support.ui import Select
from selenium import webdriver
import time
import re


#driver = webdriver.Chrome(executable_path="Chrome.exe")



#driver.get("http://bioinformatica.mty.itesm.mx:8080/Biomatec/SurvivaX.jsp")



#print driver.page_source.encode('gbk','ignore')
gene_name_list = open(r'D:\experiment working\Box Sync\Gene\genename.txt')
name_num = 1
gene_pHR_list = [['gene', ['pHR']]]

regx = re.compile('(?<![\d.])(?!\.\.)(?<![\d.][eE][+-])(?<![\d.][eE])(?<!\d[.,])'
                  '' #---------------------------------
                  '([+-]?)'
                  '(?![\d,]*?\.[\d,]*?\.[\d,]*?)'
                  '(?:0|,(?=0)|(?<!\d),)*'
                  '(?:'
                  '((?:\d(?!\.[1-9])|,(?=\d))+)[.,]?'
                  '|\.(0)'
                  '|((?<!\.)\.\d+?)'
                  '|([\d,]+\.\d+?))'
                  '0*'
                  '' #---------------------------------
                  '(?:'
                  '([eE][+-]?)(?:0|,(?=0))*'
                  '(?:'
                  '(?!0+(?=\D|\Z))((?:\d(?!\.[1-9])|,(?=\d))+)[.,]?'
                  '|((?<!\.)\.(?!0+(?=\D|\Z))\d+?)'
                  '|([\d,]+\.(?!0+(?=\D|\Z))\d+?))'
                  '0*'
                  ')?'
                  '' #---------------------------------
                  '(?![.,]?\d)')


for i in gene_name_list:
  gene_name = i
  #print gene_name
  driver = webdriver.PhantomJS(executable_path="phantomjs.exe")
  driver.get('http://bioinformatica.mty.itesm.mx:8080/Biomatec/SurvivaX.jsp')
  time.sleep(20)
  survivaX_web_test = driver.page_source.encode('ascii', 'ignore')
  # print viewer_web_test
  survivaX_web_test_name = re.findall('Hematologic',survivaX_web_test)
  #print survivaX_web_test_name


  if survivaX_web_test_name:
      #print 'The SurvivaX web has been confirmed.'

      try:

          driver.find_element_by_id('genes').send_keys(gene_name)
          driver.find_element_by_id('tissueHematologic').click()
          driver.find_element_by_id('database128').click()
          #ac = driver.find_element_by_xpath('database128')
          # #webdriver.ActionChains(driver).move_to_element(ac).click(ac).perform()
          driver.find_element_by_id('send').click()
          time.sleep(20)
          bio_vie_name = 'Biomarker Viewer'
          for handle in driver.window_handles:
            #print handle
            driver.switch_to.window(handle)
            url_title = driver.title
            #print url_title
            if url_title == bio_vie_name:
              viewer_web_test = driver.page_source.encode('ascii', 'ignore')
              #print viewer_web_test
              viewer_web_test_name = re.findall('DDDDDDDDDDDDDDDDDDDDDDDDDDDDD',viewer_web_test)
              #print 'The Biomarker Viewer web has been confirmed.'
              if viewer_web_test_name:
                  select = Select(driver.find_element_by_id('W0F0'))
                  select.select_by_value("CENSORED:FOLLOW.UP.SURVIVAL.EVENT.MONTHS")
                  driver.find_element_by_id('W0F2').click()
                  driver.find_element_by_id('WRDIV0').click()
                  time.sleep(40)
                  #print driver.page_source.encode('gbk', 'ignore')
                  current_result = driver.page_source.encode('ascii', 'ignore')

                  #for line in current_result.readlines():
                    #print line

                  name_num_Str = str(name_num)
                  gene_name_strip = gene_name.strip('\n')
                  fname = gene_name_strip + '_' + name_num_Str
                  current_file = open(fname, 'w')
                  current_file.write(current_result)
                  current_file.close()
                  #print 'The file has been saved'

                  name_num = name_num + 1
                  pHR_num = current_result.find('pHR')
                  pHR_text = current_result[pHR_num:pHR_num+40]
                  pHR = regx.findall(pHR_text)
                  total_data = [gene_name_strip,pHR]

                  current_pHR_file = open('Total_data_list_pHR', 'a+')
                  add_pHR_num = str(total_data)
                  current_pHR_file.write(add_pHR_num + '\n')

                  #print total_data
                  gene_pHR_list.append(total_data)
                  #for line in gene_pHR_list:
                      #print line
                  #print total_data


                  driver.close()
              else:
                  driver.close()
            else:
              driver.close()
          os.system('tskill phantomjs')
      finally:
          print  total_data
  else:
      os.system('tskill phantomjs')




    #print driver.page_source.encode('gbk', 'ignore')
#driver.switch_to.window(ee25d4c0-581e-11e8-b887-a1342df3af2a)
#print driver.page_source.encode('gbk', 'ignore')
#driver.switch_to.window(driver.title('Biomarker Viewer'))
#print driver.page_source.encode('gbk','ignore')
#driver.switch_to.window(2)
#print driver.page_source.encode('gbk','ignore')
#driver.get("http://bioinformatica.mty.itesm.mx:8080/Biomatec/SurvivaXvalidator.jsp")
#print driver.page_source.encode('gbk','ignore')
#a1 = driver.switch_to.alert
#time.sleep(1)
#print a1.text

#driver.execute_script("window.confirm = function(msg) { return true; }")
#driver.find_element_by_xpath('//*[@id="wrapper"]/div[2]/div/div/div[2]/div[2]/a').click()
#print(alert.text)
#driver.find_element_by_id('addButton').click()
#time.sleep(10)
#print driver.page_source.encode('gbk','ignore')

