---
layout: post
title:      "My TopBreweries CLI Project problem solving."
date:       2020-05-01 22:30:11 -0400
permalink:  my_topbreweries_cli_project_problem_solving
---


So, during these last two and a half long, LONG weeks I finally finished my project. Not without the complex problems, empty coffee pots, early mornings and late nights, etc.
My main objective was to scrape a website and return all **brewery_names**, **brewery_links**, **city**, **states**, and **descriptions**. Most were pretty straight forward like the **brewery_links/brewery_names/states** however, during the first project week someone decided it was a prime time to update their website and things got MESSED UP.
Most of the **city** were in an <em> tag but a handful were just inside the <p> tag along with the **description**. 
And the **description** contained **brewery_names** and cities as well as contained extra `\n` and `"--"` within the description. The `\n` was making new lines between **brewery_name** and **city** and the `"--"` seperated certain sentences in certain **descriptions** and all **descriptions** had initials at the end of each **description**. 
So, you might be wondering? How did you solve this problem? I wasn't alone. I had the help of some students in my cohort but ultimately relied on my teacher, Micah to help me scrape the necessary data needed to then use in my CLI. 
We ended up fixing the **city** and **description** within each other.

```
parsed_page.each.with_index do |brewery, i|
            b_links = brewery.css("a").attr("href").text
            b_name = brewery.css("a").first.text
            cityem = brewery.css("em:nth-child(3)").first
            description_unaltered = brewery.text.split('--')[0...-1].join("--")
            city =  cityem ? cityem.text : find_city(description_unaltered)
            description = description_unaltered.split("\n").last
						
			def self.find_state(des)
             des.gsub(/([^\sA-Z])([A-Z])/, '\1'+"\n"+'\2').split("\n")[1]
			end
```

So essentially what we had to do was create a **cityem** object that selected the 3rd element of <em>
Then we made a **description_unaltered** to split the text by "--" from the 1st element in the array up to the second to last element in the array and join them back up with "--"
We then create a **city** object and make it equal to cityem ?  cityem.text : find_state(description_unaltered) which is like a true/false.
Then, **description** is equal to description_unaltered.split("\n").last which splits the last "\n" off the last one (which is after city and before the description)

now, below we made a  def find_city(des) method that uses 'gsub' which takes one thing and replaces it with another. We use regex to select from the start of the line (^) and selects any whitespace character (\s) of all Capital Letters (A-Z) then runs through the first argument, finds "\n", then runs the second argument (A-Z) and splits the second element in the array by the "\n"
As complex as this sounds it worked out pretty simply. It was an enormous pain to receive all this data but a little bit of regex, splitting, and ternary operators became a huge help to get the data I needed.

