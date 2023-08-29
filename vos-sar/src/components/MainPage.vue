<template>
  <v-sheet width="300" class="mx-auto">
    <v-form @submit.prevent @click="submit">
      <v-text-field
          v-model="firstName"
          :rules="[rules.required]"
          label="Фамилия"
          variant="underlined"
      />
      <v-text-field
          v-model="lastName"
          :rules="[rules.required]"
          label="Имя"
          variant="underlined"
      />
      <v-text-field
          v-model="middleName"
          :rules="[rules.required]"
          label="Отчество"
          variant="underlined"
      />
      <v-select
          v-model="familyAmount"
          :rules="[rules.required]"
          label="Количество человек в семье"
          :items="[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]"
          variant="underlined"
      />
      <v-checkbox
          variant="underlined"
          v-model="isChildren"
          label="Есть ли дети до 18 лет?"/>
      <v-select
          :disabled="!isChildren"
          v-model="childrenUnder18"
          :rules="[rules.required]"
          label="Количество детей до 18 лет"
          :items="[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]"
          variant="underlined"
      />
      <v-text-field
          v-model="city"
          :rules="[rules.required]"
          label="Город"
          :disabled="true"
          variant="underlined"
      />
      <v-select
          v-model="area"
          :rules="[rules.required]"
          label="Район"
          :items="['Лопатинский рудник', 'Фетровая фабрика', 'Новлянский квартал', 'пос. Виноградово', 'пгт. Белоозерский', 'Золотово', 'Центр', 'Москворецкий квартал', 'Цемгигант']"
          variant="underlined"
      />
      <v-text-field
          v-model="occupation"
          :rules="[rules.required]"
          label="Род занятости"
          variant="underlined"
      />
      <v-text-field
          v-model="phone"
          :rules="[rules.phone]"
          label="Номер телефона"
          @input="formatPhoneNumber"
          variant="underlined"
      />
      <v-btn type="submit" block class="mt-2">Submit</v-btn>
    </v-form>
  </v-sheet>
</template>

<script>
export default {
  name: 'MainPage',

  data: () => ({
    firstName: '',
    lastName: '',
    middleName: '',
    familyAmount: 0,
    isChildren: false,
    childrenUnder18: 0,
    city: 'Воскресенск',
    area: '',
    occupation: '',
    phone: '',

    rules: {
        required: value => (value ? true : 'Это поле обязательно.'),
        phone: value => {
          const pattern = /^((\+7|7|8)+([0-9]){10})$/;
          return pattern.test(value) || 'Неверный формат телефона';
        },
    }
  }),

  methods: {
    formatPhoneNumber() {
      if (this.phone.length === 1 && this.phone[0] !== '+7' && this.phone[0] !== '8') {
        this.phone = '+7' + this.phone;
      } else if (this.phone.length === 0) {
        this.phone = '+7';
      } else if (this.phone[0] === '8' || this.phone[0] === '7') {
        this.phone = '+7' + this.phone.substring(1);
      }
    },

    submit() {
      const dataToSend = {
        firstName: this.firstName,
        lastName: this.lastName,
        middleName: this.middleName,
        familyAmount: this.familyAmount,
        isChildren: this.isChildren,
        childrenUnder18: this.childrenUnder18,
        city: this.city,
        area: this.area,
        occupation: this.occupation,
        phone: this.phone,
      };

      console.warn('Данные для отправки:', dataToSend);
    },
  },
};
</script>

