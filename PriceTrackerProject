import requests
from bs4 import BeautifulSoup

products_to_track = [
    {
        "product_url": "https://www.amazon.in/dp/B08ZMTJMLN/ref=s9_acss_bw_pg_test_9_i?pf_rd_m=A1K21FY43GMZF8&pf_rd_s=merchandised-search-16&pf_rd_r=WRSX1X27XS2PDPFSGGDW&pf_rd_t=101&pf_rd_p=9c64821e-71c3-4d19-a943-d93fe012e8dc&pf_rd_i=1389401031",
        "name": "Vivo V21e 5G",
        "target_price": 20000
    },
    {
        "product_url": "https://www.amazon.in/dp/B092J4F8MS/ref=s9_acss_bw_pg_test_1_i?pf_rd_m=A1K21FY43GMZF8&pf_rd_s=merchandised-search-16&pf_rd_r=WRSX1X27XS2PDPFSGGDW&pf_rd_t=101&pf_rd_p=9c64821e-71c3-4d19-a943-d93fe012e8dc&pf_rd_i=1389401031",
        "name": "Samsung Galaxy M42 5G",
        "target_price": 28000
    },
    {
        "product_url": "https://www.amazon.in/dp/B089MVC437/ref=s9_acss_bw_pg_test_10_i?pf_rd_m=A1K21FY43GMZF8&pf_rd_s=merchandised-search-16&pf_rd_r=WRSX1X27XS2PDPFSGGDW&pf_rd_t=101&pf_rd_p=9c64821e-71c3-4d19-a943-d93fe012e8dc&pf_rd_i=1389401031",
        "name": "Mi 10i 5G",
        "target_price": 26000
    },
    {
        "product_url":"https://www.amazon.in/OnePlus-Nord-Charcoal-256GB-Storage/dp/B09575YG72/ref=lp_26394213031_1_1",
        "name":"OnePlus Nord CE 5G",
        "target_price":23000
    },
    {
        "product_url":"https://www.amazon.in/dp/B07WDKLZPN/ref=s9_acss_bw_pg_test_29_i?pf_rd_m=A1K21FY43GMZF8&pf_rd_s=merchandised-search-16&pf_rd_r=MQTYZ5TZCPC66VNV190B&pf_rd_t=101&pf_rd_p=9c64821e-71c3-4d19-a943-d93fe012e8dc&pf_rd_i=1389401031",
        "name":"iQOO Z3 5G",
        "target_price":22000
    }
]


def give_product_price(URL):
    headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"
    }
    page = requests.get(URL, headers=headers)
    soup = BeautifulSoup(page.content, 'html.parser')
    product_price = soup.find(id="priceblock_dealprice")
    if (product_price is None):
        product_price = soup.find(id="priceblock_ourprice")

    return product_price.getText()


result_file = open('my_result_file.txt','w')

try:
    for every_product in products_to_track:
        product_price_returned = give_product_price(every_product.get("product_url"))
        print(product_price_returned + " - " + every_product.get("name"))

        my_product_price = product_price_returned[1:]
        my_product_price = my_product_price.replace(',', '')
        my_product_price = int(float(my_product_price))

        print(my_product_price)
        if my_product_price < every_product.get("target_price"):
            print("Available at your required price")
            result_file.write(
                every_product.get("name") + '- \t' + ' Available at Target Price' + ' Current Price - ' + str(
                    my_product_price) + '\n')
        else:
            print("Still at current price")

finally:
    result_file.close()
