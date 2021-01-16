# Find correlations within the Olist dataset
## Download and decompress Olist dataset
[Brazilian E-Commerce Public Dataset by Olist, version 7](https://www.kaggle.com/olistbr/brazilian-ecommerce/)
## Import csv files to pandas.DataFrame
    import numpy as np
    import pandas as pd
    ocu = pd.read_csv('olist/olist_customers_dataset.csv')
    ogl = pd.read_csv('olist/olist_geolocation_dataset.csv') 
    oit = pd.read_csv('olist/olist_order_items_dataset.csv')
    opa = pd.read_csv('olist/olist_order_payments_dataset.csv')
    ore = pd.read_csv('olist/olist_order_reviews_dataset.csv')
    oor = pd.read_csv('olist/olist_orders_dataset.csv')
    opr = pd.read_csv('olist/olist_products_dataset.csv')
    pcn = pd.read_csv('olist/product_category_name_translation.csv')
    j1 = pd.merge(oor, oit, on='order_id', how='left')
    j2 = pd.merge(j1, ocu, on='customer_id', how='left')
    vgl = ogl.groupby(['geolocation_zip_code_prefix', 'geolocation_city', 'geolocation_state']).mean()
    j3 = pd.merge(j2, vgl, how='left', left_on=['customer_zip_code_prefix', 'customer_city', 'customer_state'], right_index=True)
    vpg = opa.groupby('order_id').sum()
    vgl = ogl.drop_duplicates().to_numpy()
