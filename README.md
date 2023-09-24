# fragment-arguments-navigation-example
example of passing arguments with navigation

**Step 1**
Add dependency in Project-Level build.gradle

buildscript {
    dependencies {
        ...
        classpath ("androidx.navigation:navigation-safe-args-gradle-plugin:2.7.3")
    }
}

**Step 2**
Apply plugins in App-Level build.gradle

plugins {
    id("com.android.application")
    ... 
    id("androidx.navigation.safeargs")
}

**Step 3**
In Navigation file, res/navigation/mobile_navigation.xml
add action from current fragment, for example :

<fragment
        android:id="@+id/nav_transform"
        android:name="com.example.responsiveview.ui.transform.TransformFragment"
        android:label="@string/menu_transform"
        tools:layout="@layout/fragment_transform" >
        <action
            android:id="@+id/action_nav_transform_to_transform_detail"
            app:destination="@id/nav_transform_detail"/>
</fragment>

add argument for destination fragment, for example :

<fragment
        android:id="@+id/nav_transform_detail"
        android:name="com.example.responsiveview.ui.transform.TransformDetailFragment"
        android:label="@string/menu_transform_detail"
        tools:layout="@layout/fragment_transform_detail" >
        <argument
            android:name="extra_name"
            app:argType="string" />
</fragment>

**Step 3**
In current fragment file, pass the arguments like this

findNavController().navigate(TransformFragmentDirections.actionNavTransformToTransformDetail(extraName))

**Step 4**
In destination fragment file, get the arguments like this

if (arguments != null) {
            val name = arguments?.getString(EXTRA_NAME)
            binding.textName.text = name
}

