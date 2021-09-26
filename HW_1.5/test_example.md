pm.test("Body is correct", function ()  {
    pm.response.to.have.body("This is the first responce from server!");});

pm.test("Body matches string", function () {
    pm.expect(pm.response.text()).to.include("This is the first responce from server!");});

pm.test("name = abc", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.name).to.eql((request.data.name))});

const paramsString = request.url.split('?')[1];
const eachParamArray = paramsString.split('&');
let params = {};
eachParamArray.forEach((param) => {
    const key = param.split('=')[0];
    const value = param.split('=')[1];
    Object.assign(params, {[key]: value});
});
console.log(params);

let a = pm.request.url.query.all()

pm.expect(jsonData.family.pets.dog).to.have.property("name")
