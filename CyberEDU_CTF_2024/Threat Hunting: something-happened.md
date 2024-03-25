# something-happened

![image](https://github.com/alexsandusf/CTFWriteups/assets/162010016/f50e333a-3eb4-4f3a-9408-e3402d0a636c)

We are givin some Kibana logs to try and answer a few questions

![image](https://github.com/alexsandusf/CTFWriteups/assets/162010016/050e507e-605b-4c3d-b306-2a7efe9344d9)

We can go to the discover tab in Kibana and select for something-happened to start viewing the logs

# Question 1:

Almost every packet is sent to the IP 198.71.247.91 which will be the IP of the compromised host

![image](https://github.com/alexsandusf/CTFWriteups/assets/162010016/2e12069f-8a56-403f-b380-db9cc87e46f6)

# Question 2:

We can see a log4j payload to the ip target IP so the answer to the question of what attack is log4j


# Question 3:

There really isn't an easy way to get the user_agent used in the attack most people had to end up guessing to get the correct answer this question was made very poorly, but was still cool to use Kibana.

Eventually you will find the useragent is mozilla for the final question
