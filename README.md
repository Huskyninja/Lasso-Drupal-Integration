# Lasso Drupal Webform Integration
v 0.2

Integration with Drupal 7 Webform 4.x and Lasso Register API

# Requirements

- Drupal 7.x
- Webform 4.x
- cURL

# Quick Start

1. Ensure you have both Webform 4.x or greater installed on your Drupal instance and cURL installed on your host server.

2. Install the module as normal

3. Enter the Lasso target URL and any Webform IDs (comma delineated) in the Lasso Integration configuration (admin/config/content/lasso).

4. Set up your Webform's form fields so it conforms with Lasso's API and this module's Form Key requirements (see list - below). Ensure that all hidden fields are set to Hidden Element under "Display".

5. Form fields identified in Lasso's documentation call for several required fields, some as hidden fields (e.g. Lasso UID and Client ID). Ensure that all hidden fields are set to Hidden Element under "Display", as Secure Value has not been tested. Please refer to your Lasso documentation for more information.

6. Test. Be successful. Leave work early.

# More Information

This module is fairly simple in operation, and is in need of serious optimization. Upon a Webform submit, the module uses webform_alter() to capture the event, and then checks the Webform ID against an array of saved IDs. If they match, this kicks off a function where the Weform data is parsed based on the Form Key value, converting them to Lasso friendly names and values in an array. Then this Lasso friendly array is converted to a query string, and finally passed to cURL, where the query string is posted to the Lasso API. Each post is recorded to the Drupal log. (Note to self: create a de-bug option so only cURL errors are saved by default.)

Here is the list of supported Lasso query variables and their supported Webform Form Keys. I tried to ensure that their standard would conform to what Drupal will create automatically, but there is the potential for variance.

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

The following Lasso query variables are not supported.

	Questions[XXXXX]
	SignupThankyouLink
	SignupEmailLink
	SignupEmailSubject

This module was created by mlumadue for SageAge. @Copyleft - All wrongs reserved. 

This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or(at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program.  If not, see <http://www.gnu.org/licenses/>.

