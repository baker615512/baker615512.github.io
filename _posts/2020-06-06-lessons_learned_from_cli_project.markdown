---
layout: post
title:      "Lessons Learned from CLI Project"
date:       2020-06-07 02:44:28 +0000
permalink:  lessons_learned_from_cli_project
---


For my CLI project, I used an open API about Dungeons & Dragons.  I provide the user with a list of skills needed to create a character.  The skills are related to your ability scores, and your character has proficiency in the skills you choose.  In the CLI, you can select a skill to see details about it along with the ability to which it corresponds.  

### First lesson

During this project, I ran into two main challenges.  The biggest challenge I encountered came when I needed to get the details about the skill that the user selected.  The skills are numbered in my CLI, and the user would enter a numbered selection, but I needed the skill name to send to the API in order to get the details.  

```
def get_skills_details(index)
```

All skills are saved with a name in the first API call to the DndSkills class.  My first line of code in this method accesses each skill by name:

```
name = DndSkills.all[index -= 1].name
```

The second line in this method accesses another method in the DndSkills class:

```
selected_skill = DndSkills.find_by_name(name)
```

Now that I have found the object by name, I'm able to send that to my Api class:

```
Api.get_skills_details(name) unless selected_skill.has_details?
```

Now, I am able to get the skills details in the Api class by the name instead of the index.  However, the name of the skill is capitalized.  Another issue is that there is a hyphen between words if the skill has multiple words.  For instance, Sleight of Hand is the name of the skill, but the API endpoint needs to be sleight-of-hand.  To achieve this, I used the following line of code in the Api.get_skills_details(name) method:

```
res = RestClient.get("#{BASE_URL}#{name.downcase.gsub(" ", "-")}")
```

The .downcase method will change all letters to lowercase, and the .gsub method is replacing spaces with hyphens.

### Second lesson
I thought it would be smooth sailing once I resolved that issue, but I ran into an unexpected issue.  When I entered a number, the correct skill details would return, but regardless of my selection, it always returned "Acrobatics" for the skill name, which is the first skill in the array.  I was baffled.  I used binding.pry on almost every method in my gem, and then I found the problem.  In the DndSkills class, I had typed:

```
def self.find_by_name(name)
       all.detect(&:name)
    end
```

I thought this was a clever, concise way of iterating over my array of skill names.  The problem was that it returned the first object that returned true.  Therefore, I had to edit it this way:

```
def self.find_by_name(name)
       all.detect{ |skill| skill.name == name}
    end
```

I needed the name I passed in as an argument to equal the name from array of skills.

I hope this helps anyone reading to avoid similar mistakes in your own code.
