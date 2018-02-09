<script>
export default {
  props: {
    id:String, 
    classString:String, 
    required: {
      type:Boolean,
      default: false
    },
    disabled: {
      type: Boolean,
      default: false
    },
    suffix:String,
    placeholder:String,
    type:{
      type: String,
      default: 'text'
    },
    validator: {
      type: Function,
      default: null
    },
    validateWhen:{
      type:Function,
      default:model=>model.length
    },
    value:{
      required: true
    }
  },
  computed:{
    props(){return {}},
    model:{
      get(){
        return this.inputTransform(this.value);
      },
      set(value){
        this.$emit('input', this.outputTransform(value));
        if(this.validator)
          this.$emit('isValid', this.validator(value)); 
      }
    },
    validationColor(){
      return this.isValid() ? 'success' : 'error';
    }
  },
  methods:{
    isValid(){
      // se quiser validar sem transformação inputTransform, aplicar validator a this.value
      if(this.validator)
        return this.validator(this.model);

      return false;
    },
    inputTransform(value){
      return value;
    },
    outputTransform(value){
      return value;
    }
  }
}
</script>
<template src='./SimpleInput.htm'></template>
<style lang='scss' src='./SimpleInput.scss' scoped></style>
