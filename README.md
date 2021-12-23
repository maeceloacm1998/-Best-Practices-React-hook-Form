<!-- Título -->
# Melhor prática para utilizar React-Hook-Forms   ![](android/app/src/main/res/mipmap-hdpi/logo.png) 
> Exemplo de componentização de um input com a biblioteca, mantendo o código limpo ao decorrer da aplciação. 

## 🕵🏻‍♂️  Guia 
1. Inicie um projeto com react-native.
2. Instale a lib do React Hook Forms (```yarn add react-hook-form```).
3. Acesse o meu Linkedin e faça conexão comigo. 😁 [![LinkedIn][linkedin-shield]][linkedin-url1]

<!-- Exemplo -->
## 🏗 Exemplo
Em primeiro lugar, crie uma pasta para o seu componente.

```
components/
│
└─ InputForm/
│          └─ index.tsx
│          └─ styles.ts   
src/
│
└─ screens/
          └─ Formulario/  
                        └─ index.tsx
                        └─ styles.ts
```


Seu app pode ter essa estrutura ou a que você preferir. Partindo desse passo, vamos ao conteúdo de cada pasta

### InputForm - InputForm/index.tsx
A ideia desse componente será passar sempre o "name", que serve para dar referência ao seu input e o "control", que é uma forma do React-hook-forms referencia esse elemento 
com os demais e retornar o valor.

```
import React from "react";
import { TextInputProps } from "react-native";

import { Controller, Control } from "react-hook-form";

import { Container } from "./styles";

interface Props extends TextInputProps {
  name: string;
  control: Control;
}

export function InputForm({ name, control, ...rest }: Props) {
  return (
    <Controller
      control={control}
      render={({ field: { onChange, value } }) => (
        <Container onChangeText={onChange} value={value} {...rest} />
      )}
      name={name}
    />
  );
}

```

### InputForm - InputForm/styles.tsx

```
import styled from 'styled-components/native';

import { RFValue } from "react-native-responsive-fontsize";

export const Container = styled.TextInput`
  height: ${RFValue(60)}px;
  padding-left: 16px;
  border-radius: 5px;

  background-color: ${({ theme }) => theme.colors.shape};

  color: ${({ theme }) => theme.colors.text_dark};
  font-family: ${({theme}) => theme.fonts.regular};
  font-size: 16px;


  margin-bottom: 8px;
`;

```

### Formulario - screen/formulario/index.tsx
- Dentro do fomulario ou qualquer outra tela do seu app que utilize algum input, você precisa importar o ```import { useForm } from "react-hook-form"``` e o seu componente
```import { InputForm } from "../../components/Form/InputForm"```. Depois disso, chame as propriedades ```control, handleSubmit``` de ```useForm()```, pois o controler sera passado
como propriedade de cada input e o handleSubmit, sera envolvido na função ```onSubmit(data)```, que retorna os valores digitador no input, como no exemplo abaixo:

```
import React from "react";
import { useForm } from "react-hook-form";

import { Button } from "../../components/Form/Button";
import { InputForm } from "../../components/Form/InputForm";
import { SelectCategory } from "../../components/Form/SelectCategory";

import {
  Container,
  Header,
  Title,
  Form,
  Fields,
} from "./styles";

export function Register() {
  const { control, handleSubmit } = useForm();

  function onSubmit(data: any){
    console.log(data)
  }


  return (
    <Container>
      <Header>
        <Title>Cadastro</Title>
      </Header>

      <Form>
        <Fields>
          *<InputForm placeholder="Nome" control={control} name="name" />*
          *<InputForm placeholder="Preço"  control={control} name="amount" />*

          <SelectCategory />
        </Fields>

        *<Button onPress={handleSubmit(onSubmit)} />*
      </Form>
    </Container>
  );
}

```             


# Créditos
Marcelo Antônio, Desenvolvedor mobile React-Native.

<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url1]: https://www.linkedin.com/in/marcelochmendes/
[linkedin-url2]: https://www.linkedin.com/in/monique-a-rodrigues/?miniProfileUrn=urn%3Ali%3Afs_miniProfile%3AACoAADTbEtoBU2NoL-ADvXRVLcxVeOqXYwP15ig
[product-screenshot]: images/screenshot.png


