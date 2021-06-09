<template>
<select @change="OnChange()"
    v-model="selected"
    class="form-select mt-10 block w-full border p-3 rounded"
    >
    <option value="0">Select Country</option>
    <option v-for="(country, index) in countries" :key="index" :value="country.ID">
        {{country.Country}}
    </option>
</select>
</template>

<script>
export default {
    name:'CountrySelect',
    props:['countries'],
    data() {
        return {
            selected: 0,
        }
    },
    methods: {
        OnChange(){
            const country = this.countries.find((item)=> item.ID == this.selected )
            this.$emit('get-country', country)
        }
    }
}
</script>