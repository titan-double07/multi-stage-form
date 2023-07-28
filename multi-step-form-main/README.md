```````
"use client";
import Form1 from "./components/Form1";
import Form2 from "./components/Form2";
import Form3 from "./components/Form3";
import Form4 from "./components/Form4";
import { useMediaQuery } from "react-responsive";
import PracticeForm from "./components/PracticeForm";
import { nextStep, prevStep } from "./redux/features/formSlice";
import { useAppDispatch, useAppSelector } from "./redux/hooks";
import { useRef } from "react";
import { useForm } from "react-hook-form";

function Page() {
  const lg = useMediaQuery({ query: "(min-width: 1024px)" });
  const { currentStep } = useAppSelector((store) => store.form);
  const dispatch = useAppDispatch();
  const formControl = useForm();
  const { register, handleSubmit, formState,control } = formControl;
  const formRef = useRef();
  // console.log(formRef.current);
  const submitForm = (data) => {
    console.log(data);
  };
    const handleFormSubmit = () => {
      handleSubmit(submitForm)();
    };
  return (
    <div className="flex flex-col   ">
      <div className={`${!lg && "wrapper"}`}>
        <Form1
          id={1}
          currentStep={currentStep}
          submitForm={submitForm}
          handleSubmit={handleSubmit}
          register={register}
          formRef={formRef}
          control={control}
        />
        <Form2 id={2} currentStep={currentStep} formControl={formControl} />
        <Form3 id={3} currentStep={currentStep} formControl={formControl} />
        <Form4 id={4} currentStep={currentStep} formControl={formControl} />
      </div>
      <div className="btn-container bg-white h-20 mt-5 px-6  flex items-center justify-between">
        <button className={`prev btn `} onClick={() => dispatch(prevStep())}>
          Go Back
        </button>
        {/* <button type="submit" className={`next btn`} onClick={()=>formRef.current.requestSubmit()}>
          next Step
        </button> */}
        <button type="submit" className={`next btn`} onClick={handleFormSubmit}>
          next Step
        </button>
      </div>
    </div>
  );
}

export default Page;

````````
``````
"use client";
import { useEffect } from "react";
import { useForm } from "react-hook-form";

export default function Form1({ id, currentStep,register,submitForm,handleSubmit,formRef, }) {
// useEffect(() => {
//   console.log(currentStep)
  
//    }, [currentStep]);

if(currentStep!==id) return null
  return (
    <div id={id}>
      <header className="pb-5">
        <h1>Personal info</h1>
        <p>Please provide your name, email address, and phone number.</p>
      </header>
      <form
        ref={formRef}
        className="flex flex-col gap-5"
       onSubmit={handleSubmit(submitForm)}
       >
        <div className="flex flex-col gap-1  ">
          <label htmlFor="name">name</label>
          <input
            type="text"
            placeholder="e.g.Chisom Okereke"
            className="p-3 w-full border bg-white text-blue-900 focus:bg-transparent rounded-md outline-0 focus:shadow-slate-800 focus:shadow-sm focus:border-2 focus:border-blue-800"
            id="name"
            {...register("name")}
          />
        </div>
        <div className="flex flex-col gap-1 ">
          <label htmlFor="email">email address</label>
          <input
            type="email"
            placeholder="e.g.chisom@mail.com"
            className="p-3 w-full border bg-white text-blue-900 focus:bg-transparent rounded-md outline-0 focus:shadow-slate-800 focus:shadow-sm focus:border-2 focus:border-blue-800"
            id="email"
            {...register("email")}
          />
        </div>
        <div className="flex flex-col gap-1 ">
          <label htmlFor="phoneNo">phone number</label>
          <input
            type="phoneNo"
            placeholder="e.g.+234 000 000 0000"
            className="p-3 w-full border bg-white text-blue-900 focus:bg-transparent rounded-md outline-0 focus:shadow-slate-800 focus:shadow-sm focus:border-2 focus:border-blue-800"
            id="phoneNo"
            {...register("phoneNo")}
          />
        </div>
      </form>
    </div>
  );
}

``````