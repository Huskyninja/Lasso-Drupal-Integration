# Lasso Drupal Webform Integration
v 0.3.0

Integration with Drupal 7 Webform 4.x and Lasso Register API

# Requirements

- Drupal 7.x
- Webform 4.x
- cURL

#Features

- Supports multiple forms using the same target URL
- A choice between having all form submissions to be filtered based on Webform Keys or a Quickset "Submit and Pray".
- A debug mode which reports both successful and unsuccessful submissions. Useful for remote server codes.

# Quick Start

1. Ensure you have both Webform 4.x or greater installed on your Drupal instance and cURL installed on your host server.

2. Install the module as normal

3. Enter the Lasso target URL and any Webform IDs (comma delineated) in the Lasso Integration configuration (admin/config/content/lasso).

4. Set up your Webform's form fields so it conforms with Lasso's API and this module's Form Key requirements (see list - below). Ensure that all hidden fields are set to Hidden Element under "Display".

5. Form fields identified in Lasso's documentation call for several required fields, some as hidden fields (e.g. Lasso UID and Client ID). Ensure that all hidden fields are set to Hidden Element under "Display", as Secure Value has not been tested. Please refer to your Lasso documentation for more information.

6. Test. Be successful. Leave work early.

# More Information

This module is fairly simple in operation, and is in need of serious optimization. Upon a Webform submit, the module uses webform_alter() to capture the event, and then checks the Webform ID against an array of saved IDs. If they match, this kicks off a function where the Weform data is parsed based on the Form Key value, converting them to Lasso friendly names and values in an array. Then this Lasso friendly array is converted to a query string, and finally passed to cURL, where the query string is posted to the Lasso API. This will not post form fields that are not listed in the table below, so you can include additional fields for your use without upsetting Lasso.

If the Quickset option is selected from the administration screen, then the query string will contain all Webform fields using their existing Form Keys. The module will still tease out special Lasso form values (Questions, Phone, and Email) and format them correctly (see table, below). When using Quickset, it is important to match the Webform Form Key exactly to the Lasso CRM form value you are trying to map (for example: LastName for the Lasso form value LastName - see your Lasso documentation for more information). Please remember that this feature is expermental and has not been fully tested.

If the Debug option is selected, the module will report all responses from cURL, not just those that fail (from a timeout for example). This is very useful for reviewing the remote server codes and checking to make sure your final query string is properilly formatted. Remember, any time cURL gets a response, it counts as successful, so even hitting the wrong URL will look like it worked.

The first table is the list of supported Lasso query variables and their supported Webform Form Keys. I tried to ensure that their standard would conform to what Drupal will create automatically, but there is the potential for variance.

The second table is a listing of special Lasso variables and their corrsponsing Webform Form Keys. Remember, you must always match the letter case.

Please note: At this stage, the module is not configured for multiple values (i.e. NameTitle and ContactPreference) in a select field.

	Lasso Form Field Name   -   Webform Form Key
	-------------------------------------------------
	First Name              -   first_name
	Last Name               -   last_name
	Emails[Primary]         -   emails_primary
	Emails[Secondary]       -   emails_secondary
	Emails[Tertiary]        -   emails_tertiary
	Phones[Home]            -   phones_home
	Phones[Cell]            -   phones_cell
	Phones[Work]            -   phones_work
	Phones[WorkExt]         -   phones_workext
	Phones[Fax]             -   phones_fax
	Phones[Pager]           -   phones_pager
	Address                 -   address
	City                    -   city
	Province                -   province
	PostalCode              -   postal_code
	Country                 -   country
	NameTitle               -   name_title
	Company                 -   company
	ContactPreference       -   contact_preference
	Comments                -   comments
	RatingID                -   rating_id
	SourceTypeID            -   source_type_id
	SecondarySourceTypeID   -   secondary_source_type_id
	LassoUID                -   lasso_uid
	ClientID                -   client_id
	ProjectID               -   project_id
	domainAccountId			-	domain_account_id
	guid					-	guid

The Lasso query variable Questions is now supported using the following convention:

	Questions[XXXXX]		-	questions_XXXXX
	
Using Quick Set:

	Lasso Form Field Name   -   Webform Form Key
	-------------------------------------------------
	Emails[Primary]         -   Primary
	Emails[Secondary]       -   Secondary
	Emails[Tertiary]        -   Tertiary
	Phones[Home]            -   Home
	Phones[Cell]            -   Cell
	Phones[Work]            -   Work
	Phones[WorkExt]         -   Workext
	Phones[Fax]             -   Fax
	Phones[Pager]           -   Pager
	
The Questions variable works the same as stated above.	
	
The following Lasso query variables are not supported.

	SignupThankyouLink
	SignupEmailLink
	SignupEmailSubject

This module was created by Huskyninja for SageAge. @Copyleft - All wrongs reserved. 

This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or(at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program.  If not, see <http://www.gnu.org/licenses/>.

