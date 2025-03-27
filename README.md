# What

A test repo as a proof of concept for base64 decoding age encrypted files using GitHub's REST API

`key.txt` has the password `123456` and the encrypted contents of `test.age` is `test123`

Run the following to see that the base64 encoded content of this file is different from what you would expect:

```
echo "Correct base64 of file:"
cat test.age | base64
# Doing the following works as expected and produces `test123`:
# base64 test.age | base64 --decode | age --decrypt -i key.txt

echo ""

echo "What GitHub returns:"
curl -sS "https://api.github.com/repos/msmol/age-gh-b64-poc/contents/test.age" | jq -r '.content'
# Doing the following does _not_ work (but is expected since the base64 encoded string is wrong):
# curl -sS "https://api.github.com/repos/msmol/age-gh-b64-poc/contents/test.age" | jq -r '.content' | base64 --decode | age --decrypt -i key.txt
```

## Results


```
Correct base64 of file:
YWdlLWVuY3J5cHRpb24ub3JnL3YxCi0+IFgyNTUxOSBEd09HMTc3eVBBcVNXTlBOS2VZeWdhQUpP
bFVYZVNPalhhUlo2eEI4bGhnCnd6amRJRE5PdElzVitCTWRQOWN4WlNLbi9JMk5KWW00QkVvY2hM
MVliYk0KLS0tIDlmcVRiV2d6ZGVmcFI0S2hvS3A1VVJoZ2o3VHN3ZnVrTkpGQTViamVhTWcKF5yT
tyuTzfPH8S5DAnCF9I7411AbmxpvYSKjGhWDr7L6Vsatgc/I1A==

What GitHub returns:
5oWn5pSt5pWu5o2y56Ww55Gp5r2u4rmv54mn4r2244SK4rS+4oGY44i145Sx
46Sg5JG35L2H44S345255YGB54WT5Z2O5YGO5K2l5aW55p2h5IWK5L2s5ZWY
5pWT5L2q5aGh5Yma45m45Ii45rGo5pyK55265qmk5KWE5LmP55GJ542W4q2C
5LWk5YC55o245amT5K2u4r2J44mO5KmZ5rS05ImF5r2j5qGM44WZ5omi5LSK
4rSt4rSg46Wm54WU5omX5p265pGl5pmw5Yi05K2o5r2L54C15ZWS5qGn5qi3
5ZGz552m55Wr5LmK5JmB45Wi5qml5oWN5pyK4Z6c6Y634q6T7Lez7J+x4rmD
ybDol7Tou7jtnZDhrpvhqa/mhKLqjJrhloPqvrLvqZbsmq3oh4/so5Q=
```

