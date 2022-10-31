# Tutorial Inery Task 3

## Update
```
sudo apt update -y && sudo apt upgrade -y
sudo apt install -y make bzip2 automake libbz2-dev libssl-dev doxygen graphviz libgmp3-dev \
autotools-dev libicu-dev python2.7 python2.7-dev python3 python3-dev \
autoconf libtool curl zlib1g-dev sudo ruby libusb-1.0-0-dev \
libcurl4-gnutls-dev pkg-config patch llvm-7-dev clang-7 vim-common jq libncurses5 git
```

## Get binary inery.cdt tools
```
git clone https://github.com/inery-blockchain/inery.cdt
```

```
export PATH=$PATH:$HOME/inery.cdt/bin/ >> $HOME/.bash_profile
source $HOME/.bash_profile
```

## Write Code
***kagak usah di edit langsung aja salin semuanya yang dibawah***
```
sudo tee $HOME/inrcrud/inrcrud.cpp >/dev/null <<EOF
#include <inery/inery.hpp>
#include <inery/print.hpp>
#include <string>

using namespace inery;

using std::string;

class [[inery::contract]] inrcrud : public inery::contract {
  public:
    using inery::contract::contract;


        [[inery::action]] void create( uint64_t id, name user, string data ) {
            records recordstable( _self, id );
            auto existing = recordstable.find( id );
            check( existing == recordstable.end(), "record with that ID already exists" );
            check( data.size() <= 256, "data has more than 256 bytes" );

            recordstable.emplace( _self, [&]( auto& s ) {
               s.id         = id;
               s.owner      = user;
               s.data       = data;
            });

            print( "Hello, ", name{user} );
            print( "Created with data: ", data );
        }

         [[inery::action]] void read( uint64_t id ) {
            records recordstable( _self, id );
            auto existing = recordstable.find( id );
            check( existing != recordstable.end(), "record with that ID does not exist" );
            const auto& st = *existing;
            print("Data: ", st.data);
        }

        [[inery::action]] void update( uint64_t id, string data ) {
            records recordstable( _self, id );
            auto st = recordstable.find( id );
            check( st != recordstable.end(), "record with that ID does not exist" );


            recordstable.modify( st, get_self(), [&]( auto& s ) {
               s.data = data;
            });

            print("Data: ", data);
        }

            [[inery::action]] void destroy( uint64_t id ) {
            records recordstable( _self, id );
            auto existing = recordstable.find( id );
            check( existing != recordstable.end(), "record with that ID does not exist" );
            const auto& st = *existing;

            recordstable.erase( st );

            print("Record Destroyed: ", id);

        }

  private:
    struct [[inery::table]] record {
       uint64_t        id;
       name     owner;
       string          data;
       uint64_t primary_key()const { return id; }
    };

    typedef inery::multi_index<"records"_n, record> records;
 };
EOF
```

## Compile Code
```
inery-cpp $HOME/inrcrud/inrcrud.cpp -o $HOME/inrcrud/inrcrud.wasm
```

## Unlock Wallet & Set Contract
***nama-akun diganti dengan nama akun yang di web inery***
```
cline wallet unlock -n nama-akun
```
***Masukkan password wallet kalian yang udah di simpen***

```
cline set contract nama-akun ./inrcrud
```

## Create, Read, Update, Destroy Contract
***nama-akun diganti dengan nama akun yang di web inery***
```
cline push action nama-akun create '[1, "AIRDROPASC", "Salam Dari ASC"]' -p nama-akun --json
```

```
cline push action nama-akun read [1] -p nama-akun --json
```

```
cline push action nama-akun update '[ 1,  "Salam Dari ASC"]' -p nama-akun --json
```

```
cline push action nama-akun destroy [1] -p nama-akun --json
```

***Done Langsung klik Finish di web inery***
