TypeScript-Knockoutjs
=====================

Example:
<pre>
module app.models {
    export class contact {
        Id: number = 0;
        Name = ko.observable('');
        SurName = ko.observable('');
        FullName;
        constructor () {
            this.FullName = ko.computed(()=>{
                return this.Name() + " " + this.SurName();
            });
        }
    }
}
module app.viewModels{
    export class contacts {
        items = ko.observableArray([]);
        addContact(){
            this.items.push(new app.models.contact);
        };
    }
}

ko.extenders['logChange'] = (target, option)=>{
    target.subscribe(function(newValue) {
       console.log(option + ": " + newValue);
    });
    return target;
};

ko.bindingHandlers['hasFocus'] = {
    init: (element, valueAccessor)=>{
                   
    },
    update: function(element, valueAccessor) {
        var value = valueAccessor();
        if (ko.utils.unwrapObservable(value))
            element.focus();
        else
            element.blur();
    }
};
var viewModel = new app.viewModels.contacts;
ko.applyBindings(viewModel);
</pre>