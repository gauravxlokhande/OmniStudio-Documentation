# call apex method in ip Remote action.


```

global class TestClass implements Callable {
    public Object call(String action, Map<String, Object> args) {
        Map<String, Object> input = (Map<String, Object>)args.get('input');
        Map<String, Object> output = (Map<String, Object>)args.get('output');
        Map<String, Object> options = (Map<String, Object>)args.get('options');

        if (action == 'invokeMethod') {
            invokeMethod(input, output, options);  // called belowd method and passed params as needed
        } else if (action == 'getperticularaccdata') {
            getperticularaccdata(input, output); // called belowd method and passed params as needed
        }

        return null; // Adjust the return value as needed.
    }

    // Method One
    private void invokeMethod(Map<String, Object> inputMap, Map<String, Object> outMap, Map<String, Object> options) {
        List<Account> accList = [SELECT Id, Name FROM Account];
        outMap.put('AccountList', accList);
    }

    // Method Two
    private void getperticularaccdata(Map<String, Object> inputMap, Map<String, Object> outMap) {
        List<Account> accList = [SELECT Id, Name FROM Account];

        List<Account> accnewlist = new List<Account>();
        for (Account acc : accList) {
            if (acc.Name == 'Edge Communications') {
                accnewlist.add(acc);
            }
        }

        outMap.put('AccountName', accnewlist);
    }
}

```
