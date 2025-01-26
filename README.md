# Prototype-For-Urban-Eaterier
import React, { useState } from 'react';
import {
  View,
  Text,
  TextInput,
  FlatList,
  TouchableOpacity,
  StyleSheet,
  Image,
  ScrollView,
} from 'react-native';

const dummyData = [
  {
    id: '1',
    name: 'Cafe Delight',
    category: 'cafe',
    cuisine: 'American',
    location: 'Downtown',
    price: '$',
    rating: 4.5,
    image: 'https://placehold.co/100x100',
    description: 'Cozy cafe with great coffee',
  },
  {
    id: '2',
    name: 'Spice Route',
    category: 'hotel',
    cuisine: 'Indian',
    location: 'Uptown',
    price: '$$',
    rating: 4.2,
    image: 'https://placehold.co/100x100',
    description: 'Authentic Indian food',
  },
  {
    id: '3',
    name: 'Street Eats',
    category: 'street food',
    cuisine: 'Local',
    location: 'Market Square',
    price: '$',
    rating: 4.7,
    image: 'https://placehold.co/100x100',
    description: 'Delicious street food at low prices',
  },
    {
    id: '4',
    name: 'Pizza Palace',
    category: 'hotel',
    cuisine: 'Italian',
    location: 'Suburb',
    price: '$$$',
    rating: 4.0,
        image: 'https://placehold.co/100x100',
        description: 'Authentic Italian pizza and dishes'
  },
  {
    id: '5',
    name: 'Brew Hub',
    category: 'cafe',
    cuisine: 'Coffee',
    location: 'Tech Park',
    price: '$',
    rating: 4.8,
    image: 'https://placehold.co/100x100',
    description: 'Excellent coffee and light snacks'
  }

];

const App = () => {
  const [searchText, setSearchText] = useState('');
    const [selectedItem, setSelectedItem] = useState(null);


  const filteredData = dummyData.filter((item) =>
    item.name.toLowerCase().includes(searchText.toLowerCase())
  );

  const renderItem = ({ item }) => (
    <TouchableOpacity
        onPress={() => setSelectedItem(item)}
      style={styles.listItem}
    >
      <Image
        source={{ uri: item.image }}
        style={styles.listImage}
        />
      <View style={styles.listItemText}>
      <Text style={styles.itemTitle}>{item.name}</Text>
        <Text>{item.category}, {item.cuisine}</Text>
         <Text>Rating: {item.rating}</Text>
          <Text>Price: {item.price}</Text>
      </View>
    </TouchableOpacity>
  );

  const renderDetails = () => {
    if (!selectedItem) return null;

    return (
        <ScrollView style={styles.detailContainer}>
        <Image source={{ uri: selectedItem.image }} style={styles.detailImage} />
          <Text style={styles.detailTitle}>{selectedItem.name}</Text>
            <Text style={styles.detailText}>{selectedItem.category}, {selectedItem.cuisine}</Text>
        <Text style={styles.detailText}>Location: {selectedItem.location}</Text>
        <Text style={styles.detailText}>Price: {selectedItem.price}</Text>
        <Text style={styles.detailText}>Rating: {selectedItem.rating}</Text>
            <Text style={styles.detailText}>{selectedItem.description}</Text>
          <TouchableOpacity
               onPress={() => setSelectedItem(null)}
            style={styles.backButton}
          >
              <Text style={styles.backButtonText}>Back to List</Text>
            </TouchableOpacity>
      </ScrollView>
    );
  };


  return (
    <View style={styles.container}>
      <TextInput
        style={styles.searchInput}
        placeholder="Search places"
        value={searchText}
        onChangeText={(text) => setSearchText(text)}
      />
      {selectedItem ? (
        renderDetails()
      ) : (
        <FlatList
          data={filteredData}
          renderItem={renderItem}
          keyExtractor={(item) => item.id}
        />
      )}
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 16,
    backgroundColor: '#fff',
  },
  searchInput: {
    height: 40,
    borderColor: 'gray',
    borderWidth: 1,
    marginBottom: 16,
    paddingHorizontal: 8,
  },
    listItem: {
    flexDirection: 'row',
    alignItems: 'center',
    marginBottom: 10,
    padding: 10,
    borderColor: '#ccc',
    borderWidth: 1,
    borderRadius: 5,
    backgroundColor: '#f9f9f9'
  },
  listItemText: {
    flex: 1,
    marginLeft: 10,
  },
    itemTitle: {
    fontSize: 18,
    fontWeight: 'bold'
  },
    listImage: {
    width: 50,
    height: 50,
    borderRadius: 25,
    marginRight: 10,
      resizeMode:'cover',
  },
    detailContainer: {
        flex: 1,
      padding: 20
    },
    detailImage: {
    width: '100%',
    height: 200,
        resizeMode: 'cover',
        marginBottom: 10,
    },
  detailTitle: {
        fontSize: 24,
        fontWeight: 'bold',
      marginBottom: 10
    },
  detailText: {
      fontSize: 16,
      marginBottom: 5
    },
    backButton: {
      backgroundColor: '#007bff',
      padding: 10,
      borderRadius: 5,
        marginTop: 15,
    },
  backButtonText: {
      color: 'white',
    textAlign: 'center',
  }
};
