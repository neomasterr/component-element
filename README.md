Usage example

Checkbox.js
```JS
import ComponentElement from '@neomasterr/component-element';

function Checkbox($element, options = {}) {
    // inheritance
    ComponentElement.call(this, $element, options);

    this.$item = this.$element.querySelector('.js-checkboxItem');
    this.$checkbox = this.$element.querySelector('.js-checkboxInput');
    this.$checkbox.addEventListener('change', this._onChangeEvent.bind(this));

    Object.defineProperty(this, 'checked', {
        get: this.getChecked.bind(this),
        set: this.setChecked.bind(this),
    });
}

// prototype chaining
Checkbox.prototype = Object.create(ComponentElement.prototype)
Object.defineProperty(Checkbox.prototype, 'constructor', {
    value: Checkbox,
    enumerable: false,
    writable: true,
});

Checkbox.prototype.setChecked = function(state) {
    state = !!state;
    this.$checkbox.checked = state;
    this.$item.classList.toggle('is-active', state);
    this.emit('checked', state);
}

Checkbox.prototype.getChecked = function() {
    return this.$checkbox.checked;
}

Checkbox.prototype._onChangeEvent = function(e) {
    this.setChecked(this.$checkbox.checked);
}

export default Checkbox;
```

App.js
```JS
import Checkbox from './Checkbox';

document.querySelectorAll('.js-checkbox').forEach($el => {
    const checkbox = new Checkbox($el, {
        on: {
            change: (checked) => {
                console.log(checked);
            },
        },
    });

    checkbox.checked = true;
    // or
    checkbox.setChecked(true);

    return checkbox;
});
```

index.html
```HTML
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title></title>
</head>
<body>
    <div class="Checkbox">
        <div class="Checkbox-inner js-checkbox">
            <div class="Kurort-sidebar__custom-checkbox js-checkboxItem">
                <svg width="16" height="12" viewBox="0 0 16 12" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path fill-rule="evenodd" clip-rule="evenodd" d="M15.6898 0.275994C16.0897 0.656955 16.105 1.28994 15.724 1.68979L6.1966 11.6898C6.00787 11.8879 5.74621 12 5.4726 12C5.19898 12 4.93732 11.8879 4.74859 11.6898L0.275994 6.99534C-0.104967 6.59549 -0.0896484 5.96251 0.31021 5.58154C0.710069 5.20058 1.34305 5.2159 1.72401 5.61576L5.4726 9.55029L14.276 0.31021C14.657 -0.0896484 15.2899 -0.104967 15.6898 0.275994Z" fill="white"></path>
                </svg>
            </div>
            <input name="test_checkbox" type="checkbox" class="js-checkboxInput">
            <span>Test checkbox</span>
        </div>
    </div>
</body>
</html>
```