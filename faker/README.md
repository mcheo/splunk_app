This Splunk App leverage on Python Faker library to generate sample data for demo or testing.

### Usage
1. Download and install this Splunk app - Faker
2. In Splunk UI, Add Data -> Monitor -> Files & Diretories -> New Local File & Directory <br/>
   Faker app will generate json output into here $SPLUNK_HOME/etc/apps/fakedata/generated_data/fake_data.json
   Recommend you to create a new Index
3. You execute a custom command to generate fake data
```
| faker num_records=<number of records> earliest=<earliest datetime> latest=<latest datetime> fields=<list of desired fields separated by commma> <optional_custom_fields>
```

Default values if not specified:
- num_records = 10
- earliest = 24 hours ago in the format of yyyy-mm-dd HH:MM:SS
- latest = current system time in the format of yyyy-mm-dd HH:MM:SS

### Command Options

```
|faker <options>
```
| Options  | Description |
| ------------- | ------------- |
|  reset |  This will truncate the output file  |
|  info  |  To retrieve the location of the output file  |
|  setup file="<new_json_file_absolute_path> |  To setup new output file   |
|  default  |  To set the output file to default location $SPLUNK_HOME/etc/apps/faker/generated_data/fake_data.json  |

### Fields
You can refer to the full list of fields [here](https://faker.readthedocs.io/en/master/providers.html)

| Category  | fields |
| ------------- | ------------- |
| Address  | address, building_number, city, city_suffix, country, country_code, current_country, current_country_code, postcode, street_address, street_name,  street_suffix |
| Automotive  | license_plate  |
| Bank  | aba, bank_country, bban, iban, swift, swift11, swift8,   |
| Barcode  | ean, ean13, ean8, localized_ean, localized_ean13, localized_ean8 |
| Color  | color, color_name, hex_color, rgb_color, rgb_css_color, safe_color_name, safe_hex_color |
| Company  | bs, catch_phrase, company, company_suffix |
| Credit Card  | credit_card_expire, credit_card_full, credit_card_number, credit_card_provider, credit_card_security_code|
| Currency  | cryptocurrency, cryptocurrency_code, cryptocurrency_name, currency, currency_code, currency_name, currency_symbol, pricetag|
| Date Time  | (Every single line of log will have datetime, you do not need to explicitly specify this field. Use it if you need other sub date time fields) am_pm, century, date, date_of_birth, date_this_century, date_this_decade, date_this_month, date_this_year, day_of_month, day_of_week, month, month_name, time, year|
| File  | file_extension, file_name, file_path, mime_type, unix_device, unix_partition|
| Geo  | coordinate, latitude, latlng, local_latlng, location_on_land, longitude|
| Internet | ascii_company_email, ascii_email, ascii_free_email, ascii_safe_email, company_email, domain_name, domain_word, email, free_email, free_email_domain, hostname, http_method, iana_id, image_url, ipv4, ipv4_private, ipv4_public, ipv6, mac_address, nic_handle, nic_handles, port_number, ripe_id, safe_domain_name, safe_email, slug, tld, uri, uri_extension, uri_page, uri_path, url, user_name|
| Credit Card  | credit_card_expire, credit_card_full, credit_card_number, credit_card_provider, credit_card_security_code|
| Credit Card  | credit_card_expire, credit_card_full, credit_card_number, credit_card_provider, credit_card_security_code|
| ISBN  | isbn10, isbn13 |
| Job   | job |
| Lorem | paragraph, paragraphs, sentence, sentences, text, texts, word, words|
| Misc  | boolean, passwword, uuid14 | 
| Person    | first_name, first_name_female, first_name_male, first_name_nonbinary, language_name, last_name, last_name_female, last_name_male, last_name_nobinary, name, name_female, name_male, name_nonbinary, prefix, prefix_female, prefix_male, prefix_nonbinary, suffix, suffix_female, suffix_male, suffix_nonbinary|
| Phone Number  | country_calling_code, msisdn, phone_number|
| Profile   | profile, simple_profile|
| User Agent    | android_platform_token, chrome, firefox, internet_explorer, ios_platform_token, linux_platform_token, linux_processor, mac_platform_token, mac_processor, opera, safari, user_agent, windows_platform_token|


### Custom Fields
To randomly generate data from your own data set, you may use custom field approach. The custom field must has prefix "c_"

Example: Assuming you want the log's fields to consists name,email and fruit which are from your own list.
```
| faker num_records=10 fields="name,email,c_fruit" c_fruit="apple,orange,grape"
```
