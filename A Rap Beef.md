# Scenario:

Two hip-hop artists are in the midst of a musical feud. Following long-stewing tensions between the artists, they have begun taking jabs at each other through their music.

Dwake, who is signed with OWL Records, was the first to strike. His newest song was intended to insult his arch-nemesis, Present, who is signed with Dollar Currency Records. However, he made a crucial mistake in his verse that took the feud in a different direction.

As a Security Analyst for OWL Records, your job is to keep the company's information safe so your artists don't get exposed during this ongoing feud.

# Objective:

1. Identify Elements of a phishing campaign
2. Interpret Security Logs to identify evidence of malicious activity 
3. Investigate a basic cybersecurity intrusion 

# Resources:

https://kc7cyber.com/challenges/187

# Questions:

## Section 1 - Enough beef for a burger:

Question 1: **Type `ready` to get started**

Answer 1: ready

---

After dropping this verse, Dwake had everyone on social media talking and laughing at Present.

```
🎶 Yo, Present, you don't know where I'm from,
Got the Washington name from my mom's side, son.
It makes sense why they call you present
Cause you're so easy to beat, its pretty much a gift
Used to play with little Fluffy, now I'm runnin' with the wolves,
You say you're on top, but I'm breakin' all the rules.
I'm on that next level, you're stuck in the past,
with those weak beats you won't last.
🎶
```

Q2: **Type `barz` to continue**

A2: barz

---

In a fit of anger, Present asked his label, Dollar Currency Records (DCR), to dig up some dirt on Dwake that he could use to retaliate.

Your homeboy (who works in the cyber underground) gave you a tip that you might see nefarious cyber activity as a result.

After sliding him a crisp $20 bill, he recounted a rumor he heard that DCR had hired a hacker who used the IP `18.66.52.227` to poke around your website in early April.

Q3: **Type `thanks dawg` to continue**

A3: thanks dawg

---

At this point, we'll start digging into the company's data to find clues that will help us solve the mysteries at hand.

We'll use KQL (Kusto Query Language) queries to manipulate our data. Don't worry, we'll provide all the queries in this game, so you don't need to learn how to write them yourself… yet.

For each query we provide, you can simply copy and paste it into the query pane on the right, and then click `run`. You can use the `control-v` shortcut to paste.

![](https://kc7photos.blob.core.windows.net/gifs/click%20to%20run.gif)

Let's take this for a spin. The following query searches for all information about the CEO of OWL Records.

Q4: What is the name of the OWL records CEO?

![image](https://github.com/user-attachments/assets/d77672fa-2bbd-4d55-bd62-7fafdded56bd)


A4: Sean Crater

---

You can use the following query to search for browsing activity to your company's website.

```jsx
InboundNetworkEvents
| where timestamp between (datetime("2024-04-10T00:00:00") .. datetime("2024-04-11T00:00:00"))
| where src_ip has "18.66.52.227"
```

Q5: How many results (rows) did you get back?

Note: You can run multiple queries on the same pane. Just be sure to put a space in between them. For example:

![image](https://github.com/user-attachments/assets/e2c83f97-38c6-4771-99ee-c96fe027fe3f)


Then simply click on the query you want to run and make sure the whole thing is highlighted.

![image](https://github.com/user-attachments/assets/309d1be5-6922-4a02-a55a-cbcc1cf890a4)


A5: 19

---

The results you are looking at represent someone browsing and searching for information on OWL Records' website.

This operator (person browsing the website) was clearly looking to find information about various artists who work for OWL Records, especially Dwake. Thanks to the homie, it looks like we are on the right path.

Here we want you to read carefully through the logs to see what the bad guys were searching for.

**Q6: What piece of information were they looking to get for Dwake? (two words - might be used for communication)**

![image](https://github.com/user-attachments/assets/c63120d9-fabf-4b51-a699-6759ecbe33a8)


A6: email address

---

Let's continue to look at the results from the previous query.

The operator here also expressed their strong opinions about Dwake's music.

**Q7: The operator is wondering why Dwake's music is so _**

![image](https://github.com/user-attachments/assets/144704f0-03f7-4063-a58b-4cba539a5990)


A7: trassshhhh or trash

---

Let's continue to look at these logs. At some point the operator discovered Dwake's email address.

**Q8: What is Dwake's email address? -** You can look at the results from the previous query to find it!

![image](https://github.com/user-attachments/assets/07a3b94a-9acc-4787-a8ba-edb7bfedd227)


A8: dwake_audrey@owl-records.com

---

The operator then attempted to take over Dwake's account by resetting his password. We know this because of the `reset-password` parameter in that last `url` they accessed.

When employees at OWL records need to reset their passwords, they must answer a set of challenge questions to prove who they are. These are the challenge questions offered on the OWL records website:

1. What is your mother's maiden name?
2. What street did you grow up on as a child?
3. What is your childhood pet's name?
4. What is the color of your first car?

Holy smokes! It looks like Dwake may have inadvertently disclosed some of this information in his last verse.

```
🎶 Yo, Present, you don't know where I'm from,
Got the Washington name from my mom's side, son.
It makes sense why they call you present
Cause you're so easy to beat, its pretty much a gift
Used to play with little Fluffy, now I'm runnin' with the wolves,
You say you're on top, but I'm breakin' all the rules.
I'm on that next level, you're stuck in the past,
with those weak beats you won't last.
🎶
```

**Q9: Which of the following did Dwake disclose in his verse? (pick one)**

A9: 1 and 3

---

Looking at the verse, let's try to figure out what values the operator may have tried to use to reset Dwake's password.

```
🎶 Yo, Present, you don't know where I'm from,
Got the Washington name from my mom's side, son.
It makes sense why they call you present
Cause you're so easy to beat, its pretty much a gift
Used to play with little Fluffy, now I'm runnin' with the wolves,
You say you're on top, but I'm breakin' all the rules.
I'm on that next level, you're stuck in the past,
with those weak beats you won't last.
🎶
```

Q10: **What is Dwake's mother's maiden name?**

A10: Washington

---

Dwake also reveals the name of his childhood pet

```
🎶 Yo, Present, you don't know where I'm from,
Got the Washington name from my mom's side, son.
It makes sense why they call you present
Cause you're so easy to beat, its pretty much a gift
Used to play with little Fluffy, now I'm runnin' with the wolves,
You say you're on top, but I'm breakin' all the rules.
I'm on that next level, you're stuck in the past,
with those weak beats you won't last.
🎶
```

Q11: **What is the name of Dwake's childhood pet?**

A11: Fluffy

---

The operator used these bits of information to reset Dwake's password. Using the query from before, we can actually see the adversary doing this.

```
InboundNetworkEvents
| where timestamp between (datetime("2024-04-10T00:00:00") .. datetime("2024-04-11T00:00:00"))
| where url has_any("washington", "fluffy")
| where src_ip has "18.66.52.227"
```

Q12: Copy and paste the full URL that shows the operator resetting the password to Dwake’s account.

![image](https://github.com/user-attachments/assets/e632e341-7f5b-485d-bcde-2239613cc1c5)


A12: [https://owl-records.com/account/security-questions?question_1=mother's+maiden+name&answer_1=Washington&question_2=first+pet's+name&answer_2=Fluffy](https://owl-records.com/account/security-questions?question_1=mother%27s+maiden+name&answer_1=Washington&question_2=first+pet%27s+name&answer_2=Fluffy)

---

After taking over Dwake's email account, the operator was able to reset the password of Dwake's Instagram account as well.

The following day, the adversaries posted an embarrassing image to Drake's Instagram.

![](https://kc7photos.blob.core.windows.net/manualphotos/rap_beef_fake_insta.png)

**Q13: Type `oh lawd` to take credit**

A13: oh lawd

# Section 2: Less beef, more phish

The higher ups at OWL records deliberated the happening in a private meeting. In that meeting was Dwake himself who was seething about what had taken place.

After 6 hours of deliberation, the company declared it a settled issue. However, they never officially specified how they dealt with the situation.

The following day, a random hacker on the dark web threatened to release damaging information on Present the rapper, if he did not announce his retirement in the next 30 days.

![image.png](attachment:31cd27f8-d4a4-4db0-9545-2730297b9d94:image.png)

Q1: **Enter `darkweb` to continue**

A1: darkweb

---

You can't prove OWL Record management had anything to do with the dark web post (nor do you have any incentive to do so), however you understand that this will spell more trouble for you.

You go back and talk to the homie, and he suggests that any retaliation would happen via phishing. This is a vague hint, but you can surely do something with this.

**Q2: Type `lesdoit` to continue**

Q2: lesdoit

---

Let's find the phish!

We already know one thing about the adversary! They used IP `18.66.52.227` in their operations. If we can find a domain name associated with this IP, it may lead us to the phishing emails.

We can look in the PassiveDNS table for ip <-> domain relationships.

```
PassiveDns
| where ip == "18.66.52.227"
```

**Q3: What domain did IP `18.66.52.227` resolve to?**

![image.png](attachment:7e2bbc5a-a018-4380-adb3-e8b5f7c5ad23:image.png)

A3: betterlyrics4u.com

---

Woohoo! We have a domain name! Things will be a lot smoother from here on out! Let's look in email logs for evidence that this domain was used.

First we'll take a quick gander at the email logs. We can use the take operator to look at ten random rows.

```
Email
| take 10
```

Q4: **Which column in the email table is most likely to contain our domain?**

![image.png](attachment:856caa9b-d81a-4994-a9b1-64268c4529d3:image.png)

A4: link

---

Great now let's look for the domain in that column.

```
Email
| where link has "betterlyrics4u.com"
```

Q5: How many results did we get from this query?

![image.png](attachment:9e6cda81-c8f6-4aef-baf8-3d3117fcc217:image.png)

A5: 13

---

Oh no! We've been phished!

Each of these rows represent an email that was sent to someone at OWL records!

**Q6: Which email address was used to send most of these emails?**

Hint: use the query from the previous question.

![image.png](attachment:24582a0c-78c4-449e-ac5b-fafb0a885335:image.png)

A6: ghostwritersanonymous@protonmail.com

---

Q7: **What was the other email address used to send these phishing emails?**

![image.png](attachment:8122996d-174c-43d6-b22b-a88420210152:image.png)

A7: wemakebeatz@gmail.com

---

It looks like the adversaries were targeting users with very particular roles.

```
let _targets = Email
| where link has "[betterlyrics4u.com](http://betterlyrics4u.com/)"
| distinct recipient;
Employees
| where email_addr in (_targets)
```

**Q8: Which role was targeted the most of all?**

![image.png](attachment:413ab521-0eeb-4043-848c-57f4bf78d5fe:image.png)

A8:Rapper

---

There was one additional role that was targeted.

**Q9: Which role (other than Rapper) was targeted by this phishing campaign?**

![image.png](attachment:5bef783b-b49c-4a12-a933-62a2a094aaef:image.png)

A9: Lead Rapper

---

Q10: **And what is the name of the Lead Rapper?**

![image.png](attachment:daf1fc96-ba18-4d12-8b64-97f21e63fc6a:image.png)

Q10: Dwake Audrey

---

Q11: What is Dwake’s IP address?

![image.png](attachment:50474e89-4c49-451b-aeee-d445c8b73a2e:image.png)

A: 10.10.0.5

---

Let's take a look at those emails again!

```
Email
| where link has "betterlyrics4u.com"
```

Q12: **What was the subject of the email sent to Dwake?**

![image.png](attachment:99da0341-62d1-46ee-bd41-bf2dd73c21ac:image.png)

A12:[EXTERNAL] RE: Need a ghostwriter for your next hit?

---

It's likely the adversaries want Dwake to click on a link and feed them his credentials.

Q13: What link did the adversaries include in their phishing email targeting Dwake?

![image.png](attachment:c9466a83-7c75-41ca-a3ba-cecec98f886e:image.png)

A13:http://betterlyrics4u.com/share/online/published/enter

---

On occasion, our email security product will block suspicious email. In those cases, the end users will never even see the suspicious emails.

**Q:14: What was the verdict of the email sent to Dwake?**

![image.png](attachment:01be8277-dcdf-4d1b-8abd-6e730ad3b4d3:image.png)

A14: CLEAN

---

Here is the phishing email Dwake was presented with.

That's pretty convincing.

![](https://kc7photos.blob.core.windows.net/manualphotos/rapbeef_phishing_email.png)

**Q:15: What name (or nickname) did the aversaries sign the email with?**

A15: GhostWriter

---

Drats! So much for that expensive email security product. So it looks like the email actually hit Dwake's inbox. But did he click it???

OutboundNetworkEvents have a record of every link that gets clicked on the OWL Record network. So if Dwake clicked on the link in email, we would see it in that data source.

We'll look in OutboundNetworkEvents for Dwake's IP address and the link he was sent.

```
OutboundNetworkEvents
| where url == "http://betterlyrics4u.com/share/online/published/enter"
| where src_ip == "10.10.0.5"
```

**Q16: When did Dwake click on the link in email? (copy and paste the time exactly)**

![image.png](attachment:6e33250d-591a-452e-b31e-5dd34b6dcb3e:image.png)

A16: 2024-04-15T12:03:12.000Z

---

After Dwake clicked on the link in the email he was presented with this phishing page:

![](https://kc7photos.blob.core.windows.net/manualphotos/rap_beef_phishing_page.png)

It is most likely he entered his username and password.

**Q17: What is written in the submit button for this login portal?**

A17: login to speak with ghost writer

---

Now that they have his credentials, the adversaries would need to validate them by logging into Dwake's account.

We can look in Authentication events to see if the adversaries were able to login to Dwake's account

```
AuthenticationEvents
| where username == "dwaudrey"
| where src_ip == "18.66.52.227"
```

Q18: **When did the adversaries attempt to login to Dwake's account?**

![image.png](attachment:5904fa0a-998a-46f0-aff5-ee9b1d99f67d:image.png)

A18: 20

24-04-15T13:03:12.000Z

---

Q19: **What was the result of this authentication attempt?**

![image.png](attachment:44237695-511f-4be1-9a5d-e6dcb7388cb6:image.png)

A19: Successful Login

---

Now that the adversaries have logged into Dwake's account, they will want to look for important information to steal.

Since we already know the adversary's IP address, we can simply check the InboundNetwork events for activity against Dwake's account

```
InboundNetworkEvents
| where timestamp between (datetime("2024-04-12T00:00:00") .. datetime("2024-05-01T00:00:00"))
| where url has "dwaudrey" 
| where src_ip has "18.66.52.227"
```

Q20: How many results did we get?

![image.png](attachment:0dcf9118-23e8-4b68-b897-4c9700ec6680:image.png)

A20: 10

---

Looks like the adversaries were searching in Dwake's email for sensitive and scandalous information.

And it looks like they got what they wanted at the end.

**Q21: What was the name of the zip file they used to steal information from Dwake's account?**

![image.png](attachment:457444db-7d9d-44b1-b1ec-e648907ebd8d:image.png)

A21:DwakesDirtySecrets.zip

---

Dwake and Present now have more than enough dirt on each other. After some deliberation facilitated by intermediary parties, they agreed to a truce.

All is balanced in the Rap World now. Until next time!

**Q22: Enter `less hack more love` to finish**

A22: less hack more love

---

# Lessons Learned:

1.
