export default class StringSchema {
constructor(validator = [(item) => typeof item == 'string']) {
this.validators = [...validator];

}

isValid(item) {|
return this.validators.every((validator) => validator(item) === true);
}
hasSpaces(){
return new StringScheme([...this.validators, (item) => item.includes(' ')]);
 }
}



export derautt Ctass Functionscnema +
constructor(validator = [(item) => typeof item == 'function'], context = {}, value = null
this.validators = [...validator];
this.context = context;
this.value = value;
this.args = args;

isValid(func) {
if (this.value) {

if (typeof func == 'function') |
| Feturn func.call(this.context, ...this.args) === this.value;
3
‘return false;
}

return this.validators.every((validator) => validator(func) === true);



isValid(func) {
if (this.value) {

if (typeof func == 'function') {

return func.call(this.context, ...this.args) === this.value;
+
return false;

+

tor) => validator(func) === true);

@ return this.val

}

callWith(context) {
return new FunctionSchema(this.validators, context, this.value, this.args);

}

expect(value) {
return new FunctionSchema(this.validators, this.context, value, this.args);

}

arguments(...args) {
return new FunctionSchema(this.validators, this.context, this.value, args);

}

Object Schema
constructor(validator) {
this.validators = validator;
}

shape(fields) {
return new ObjectSchema(fields) ;
}

isValid(value) {
const keys = Object. keys (value) ;

if (keys. length !== Object.keys(this.validators).length) {
return false;
}

const check = (obj, key, validators) => {
if (typeof obj === ‘object’ && !Array.isArray(obj) && obj !== null) {
const keys = Object. keys(obj);

return keys.map((key) => check(obj [key], key, validators [key]));
ap

return validators [key].isValid(obj);
};





import FunctionSchema from "./FunctionSchema";
import ObjectSchema from "./0bjectSchema'';
import StringSchema from ",/StringSchema’';

export default class Validator {

string() {
return new StringSchema();

+

function() {
return new FunctionSchema();

}

object() {
return new ObjectSchema();
}
ie











