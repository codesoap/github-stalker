Some scripts I threw together, to find out about organizations of
the people, that starred a github repo. I use these to find potentially
interesting employers.

# Dependencies
- Beautiful Soup (for python3)

# Performance
I did not put any effort into performance optimization. I've listed
rough performance on my system below:

- `list_stargazers` -> ~50/s
- `list_organizations` -> checking organizations of ~1user/s 
- `filter_organizations_by_member_count` -> checks filter on ~1organization/s 

As you can see it's somewhat slow right now. If better perfomance
is needed, the HTTP requests could be parallelized.

# Example usage
```
./list_stargazers 'chneukirchen/mblaze' > stargazers
cat stargazers | ./list_organizations > organizations
cat organizations |\
	awk '{print $1}' |\
	sort -u |\
	./filter_organizations_by_member_count > large_organizations
less large_organizations

# If you want to check out the organizations:
cat large_organizations | xargs -I '{}' firefox --new-tab 'https://www.github.com/{}'
```
