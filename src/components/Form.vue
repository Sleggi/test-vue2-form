<template>
  <FormulateForm v-model="formValues" @submit="handleSubmit" name="createUser">
    <div class="form__attributes attributes">
      <h1 class="title">Атрибуты формы</h1>
      <div class="attributes__wrapper">
        <div class="attributes__top">
          <FormulateInput
            name="secondName"
            label="Фамилия *"
            validation="^required|between:1,30"
            :validation-messages="{
              required: 'Поле не может быть пустым',
              between: 'От 1 до 30 символов',
            }"
          />
          <FormulateInput
            name="name"
            label="Имя *"
            validation="^required|between:1,30"
            :validation-messages="{
              required: 'Поле не может быть пустым',
              between: 'От 1 до 30 символов',
            }"
          />
          <FormulateInput
            name="patronymic"
            label="Отчество *"
            validation="^required|between:1,30"
            :validation-messages="{
              required: 'Поле не может быть пустым',
              between: 'От 1 до 30 символов',
            }"
          />
        </div>
        <div class="attributes__middle">
          <FormulateInput
            type="date"
            name="birthdate"
            label="Дата рождения *"
            validation="^required|before:10/10/2020"
            :validation-messages="{
              required: 'Заполните поле',
              before: 'Укажите действительную дату рождения',
              min: 'Введите верную дату рождения',
            }"
          />
          <FormulateInput
            name="phone"
            label="Номер телефона *"
            validation="^required|number|between:1,11,length|starts_with:7"
            :validation-messages="{
              required: 'Поле не может быть пустым',
              starts_with: 'Введите номер телефона начиная с 7',
              between: 'Номер телефона должен состоять из 11 цифр',
              number: 'Номер телефона может состоять только из цифр',
            }"
          />
          <FormulateInput
            name="gender"
            label="Пол"
            placeholder="муж/жен/другое"
            validation="optional|matches:муж,жен"
            :validation-messages="{
              matches: 'Выберите пол: муж или жен или другое',
            }"
          />
        </div>
        <div class="attributes__bottom">
          <label for="multiselect" class="formulate-input-label"
            >Выберите группу</label
          >
          <multiselect
            class="formulate-input-wrapper"
            id="multiselect"
            track-by="name"
            v-model="formValues.clientGroup"
            :options="clientGroupOptions"
            :close-on-select="false"
            multiple
            placeholder="Выберите группу"
            label="name"
          >
          </multiselect>
          <FormulateInput
            :options="{
              name1: 'Иванов',
              name2: 'Захаров',
              name3: 'Чернышева',
            }"
            type="select"
            placeholder="Лечащий врач"
            label="Лечащий врач"
            name="doctor"
          />
          <FormulateInput
            type="checkbox"
            label="Не отправлять СМС"
            name="textMessage"
          />
        </div>
      </div>
    </div>
    <div class="form__address">
      <h1 class="title">Адрес</h1>
      <FormulateInput
        name="index"
        label="Индекс"
        validation="optional|number"
        :validation-messages="{
          number: 'почтовый индекс (0-9)',
        }"
      />
      <FormulateInput
        name="country"
        label="Страна"
        validation="optional|between:1,20"
        :validation-messages="{
          between: 'От 1 до 20 символов',
        }"
      />
      <FormulateInput
        name="oblast"
        label="Область"
        validation="optional|between:1,20"
        :validation-messages="{
          between: 'От 1 до 20 символов',
        }"
      />
      <FormulateInput
        name="city"
        label="Город *"
        validation="^required|between:1,20"
        :validation-messages="{
          required: 'Поле не может быть пустым',
          between: 'От 1 до 20 символов',
        }"
      />
      <FormulateInput
        name="street"
        label="Улица"
        validation="optional|between:1,20"
        :validation-messages="{
          between: 'От 1 до 20 символов',
        }"
      />
      <FormulateInput
        name="houseNum"
        label="Дом"
        validation="optional|number"
        :validation-messages="{
          number: 'номер дома (0-9)',
        }"
      />
    </div>
    <div class="form__document">
      <h1 class="title">Паспорт</h1>
      <FormulateInput
        :options="{
          type1: 'Паспорт',
          type2: 'Свидетельство о рождении',
          type3: 'Вод.удостоверение',
        }"
        type="select"
        placeholder="Тип документа "
        label="Тип документа *"
        name="documentType"
        validation="^required"
        :validation-messages="{
          required: 'Поле обязательно для заполнения',
        }"
      />
      <FormulateInput
        name="documentSeries"
        label="Серия"
        validation="optional|number"
        :validation-messages="{
          number: 'серия (0-9)',
        }"
      />
      <FormulateInput
        name="documentNumber"
        label="Номер"
        validation="optional|number"
        :validation-messages="{
          number: 'номер (0-9)',
        }"
      />
      <FormulateInput name="documentIssued" label="Кем выдан" />
      <FormulateInput
        type="date"
        name="documentDate"
        label="Дата выдачи *"
        validation="^required|before:10/10/2020"
        :validation-messages="{
          required: 'Заполните поле',
          before: 'Укажите действительную дату выдачи',
        }"
      />
    </div>

    <FormulateInput type="submit" label="Отправить форму" />
    <h1 v-if="showModal" class="form__submited">Форма успешно отправлена</h1>
  </FormulateForm>
</template>


<script>
import Multiselect from "vue-multiselect";
export default {
  components: { Multiselect },
  data: () => ({
    showModal: false,
    formValues: { clientGroup: [] },
    clientGroupOptions: [
      { name: "VIP", value: "vip" },
      { name: "Проблемные", value: "проблемные" },
      { name: "ОМС", value: "омс" },
    ],
  }),
  methods: {
    handleSubmit() {
      this.showModal = true;
      this.$formulate.reset("createUser");
      this.$formulate.resetValidation("createUser");
      this.formValues = {};
    },
  },
};
</script>

<style  >
.formulate-form {
  max-width: 600px;
  width: 100%;
  background: #fff;
  margin: 4em auto;
  box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.125);
  padding: 2.5em;
  position: relative;
}

.title {
  font-size: 1.8em;
  letter-spacing: 0.06em;
  margin-bottom: 1em;
  color: #fec107;
  text-transform: uppercase;
  text-align: center;
}

.form__submited {
  font-size: 1.6em;
  color: #fec107;
}

.attributes__top,
.attributes__middle,
.attributes__bottom,
.form__address,
.form__document {
  margin-bottom: 1.5rem;
}
</style>